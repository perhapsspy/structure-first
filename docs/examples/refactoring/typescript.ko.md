# TypeScript Example

[Korean](typescript.ko.md) | [English](typescript.md)


## Problem
대시보드 액션 처리에서 입력 검증, 조회, 권한 판단, patch 적용, 저장, 이벤트 발행이 한 함수에 몰려 타입 안정성은 있어도 변경 안전성이 낮은 상태.

## Before

```ts
export async function runDashboardAction(input: unknown, deps: Deps) {
  const parsed = parseInput(input as any);
  let reason: string = 'invalid_input';
  if (!parsed.ok) {
    return { ok: false, reason } as const;
  }

  const user = await deps.userRepo.find(parsed.value.userId);
  const board = await deps.boardRepo.find(parsed.value.boardId);
  if (!user || !board) {
    reason = 'resource_not_found';
    return { ok: false, reason } as const;
  }
  if (board.deletedAt) return { ok: false, reason: 'board_archived' } as const;

  const canEdit = user.roles?.includes('editor') || board.ownerId === user.id || Boolean(parsed.value.force);
  if (!canEdit) {
    await deps.audit.log('dashboard_denied', {
      userId: user.id,
      boardId: board.id,
      patch: parsed.value.patch,
    });
    reason = 'forbidden';
    return { ok: false, reason } as const;
  }

  const patch = parsed.value.patch || {};
  if (!patch || (typeof patch !== 'object')) {
    reason = 'invalid_patch';
    return { ok: false, reason } as const;
  }

  let widgets = [...board.widgets];
  const removed: string[] = [];

  if (Array.isArray(patch.removeIds)) {
    widgets = widgets.filter((w) => {
      const shouldRemove = patch.removeIds.includes(w.id);
      if (shouldRemove) removed.push(w.id);
      return !shouldRemove;
    });
  }

  if (Array.isArray(patch.upserts)) {
    for (const next of patch.upserts) {
      if (!next || !next.id) continue;
      const idx = widgets.findIndex((w) => w.id === next.id);
      if (idx >= 0) {
        widgets[idx] = { ...widgets[idx], ...next };
      } else {
        widgets.push(next as any);
      }
    }
  }
  if (Array.isArray((patch as any).replaceAll)) {
    // 신규 요구사항이 기존 patch 포맷에 덧붙음
    widgets = (patch as any).replaceAll;
  }
  if (removed.length > 0 && deps.metrics) {
    deps.metrics.count('dashboard.widgets_removed', removed.length);
  }

  // 오래된 위젯 정리 정책이 액션 안에 있음
  if (parsed.value.pruneOld) {
    widgets = widgets.filter((w: any) => {
      if (!w.updatedAt) return true;
      return Date.now() - Number(new Date(w.updatedAt)) < 1000 * 60 * 60 * 24 * 30;
    });
  }

  const saved = await deps.boardRepo.save(board.id, widgets);
  if (parsed.value.touchView) {
    await deps.boardRepo.updateViewMeta(board.id, { updatedBy: user.id, at: Date.now() });
  }

  try {
    await deps.eventBus.publish('dashboard.updated', {
      boardId: saved.id,
      by: user.id,
      widgetCount: widgets.length,
    });
  } catch {
    await deps.audit.log('dashboard_event_failed', { boardId: saved.id });
  }
  if (parsed.value.notify && user.email) {
    try {
      await deps.mailer.send(user.email, 'dashboard_updated');
    } catch {
      await deps.audit.log('dashboard_notify_failed', { userId: user.id, boardId: saved.id });
    }
  }

  return { ok: true, value: saved } as const;
}
```

## After (Applied with structure-first)

```ts
type ActionResult =
  | { ok: true; value: Board }
  | { ok: false; reason: 'invalid_input' | 'resource_not_found' | 'board_archived' | 'forbidden' | 'invalid_patch' };

export async function runDashboardAction(input: unknown, deps: Deps): Promise<ActionResult> {
  const req = parseDashboardAction(input);
  if (!req.ok) return fail('invalid_input');

  const context = await loadDashboardContext(req.value, deps);
  if (!context.ok) return fail(context.reason);

  const decision = decideDashboardUpdate(context.value);
  if (!decision.ok) return fail(decision.reason);

  const saved = await persistDashboardUpdate(decision.value, deps);
  await publishDashboardUpdated(saved.id, context.value.user.id, deps);
  await sendDashboardUpdatedIfNeeded(req.value.notify, context.value.user.email, deps);

  return { ok: true, value: saved };
}

function decideDashboardUpdate(ctx: DashboardContext):
  | { ok: true; value: PersistDashboardInput }
  | { ok: false; reason: 'forbidden' | 'invalid_patch' } {
  if (!ctx.permission.canEdit) return fail('forbidden');
  if (!isValidPatch(ctx.request.patch)) return fail('invalid_patch');

  let widgets = applyWidgetPatch(ctx.board.widgets, ctx.request.patch);
  if (ctx.request.pruneOld) widgets = pruneOldWidgets(widgets, Date.now());

  return { ok: true, value: { boardId: ctx.board.id, widgets, actorId: ctx.user.id, touchView: ctx.request.touchView } };
}
```

## Interpretation

- Primary Flow: `parse -> load -> decide -> persist -> publish -> notify`
- Boundary(I/O): `loadDashboardContext`, `persistDashboardUpdate`, `publishDashboardUpdated`, `sendDashboardUpdatedIfNeeded`
- Atom(domain): `decideDashboardUpdate`, `applyWidgetPatch`, `pruneOldWidgets`, `isValidPatch`
- 읽기 기준 변화: 정책 판단과 부작용 호출이 분리되어, 실패 사유와 성공 흐름을 위에서 바로 따라갈 수 있다.
