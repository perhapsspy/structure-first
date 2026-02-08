# JavaScript Example

[Korean](javascript.ko.md) | [English](javascript.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


## Problem
The dashboard build function handles lookup, filtering, sorting, view composition, cache, and analytics at once, so UI requirement changes often trigger side effects.

## Before

```js
export async function buildDashboard(userId, filters, deps) {
  const startedAt = Date.now();
  const user = await deps.userApi.getUser(userId);
  if (!user) return { ok: false, reason: 'user_not_found' };
  if (user.status !== 'active') return { ok: false, reason: 'inactive_user' };

  let tickets = await deps.ticketApi.listTickets(user.teamId);
  if (!Array.isArray(tickets)) tickets = [];
  if (filters && filters.teamId && filters.teamId !== user.teamId) {
    // Existing admin exception was added here
    if (!user.roles?.includes('admin')) return { ok: false, reason: 'forbidden' };
    tickets = await deps.ticketApi.listTickets(filters.teamId);
  }

  if (filters && filters.onlyOpen) {
    tickets = tickets.filter((t) => t.status === 'open');
  }
  if (filters && filters.assigneeId) {
    tickets = tickets.filter((t) => t.assigneeId === filters.assigneeId);
  }
  if (filters && filters.search) {
    const q = String(filters.search).trim().toLowerCase();
    tickets = tickets.filter((t) => String(t.title || '').toLowerCase().includes(q));
  }
  if (filters && filters.priority) {
    tickets = tickets.filter((t) => t.priority === filters.priority);
  }
  if (filters && filters.excludeMuted) {
    tickets = tickets.filter((t) => !t.muted);
  }

  const summary = {
    total: tickets.length,
    open: tickets.filter((t) => t.status === 'open').length,
    urgent: tickets.filter((t) => t.priority === 'p1').length,
  };
  if (filters && Number.isInteger(filters.limit) && filters.limit > 0) {
    tickets = tickets.slice(0, filters.limit);
  }

  const recent = tickets
    .slice()
    .sort((a, b) => Date.parse(b.updatedAt || 0) - Date.parse(a.updatedAt || 0))
    .slice(0, 5);

  const view = {
    user: { id: user.id, name: user.name },
    summary,
    recent,
  };

  try {
    await deps.cache.set(`dashboard:${userId}`, view);
  } catch (e) {
    deps.logger.warn('cache_set_failed', { userId });
    // Cache failure fallback read is also handled here
    try {
      const fallback = await deps.cache.get(`dashboard:${userId}`);
      if (fallback && fallback.summary) view.summary.lastCacheHit = true;
    } catch (_) {}
  }

  try {
    await deps.analytics.track('dashboard_viewed', {
      userId,
      total: summary.total,
      urgent: summary.urgent,
      hasSearch: Boolean(filters && filters.search),
    });
  } catch (e) {
    // Ignore analytics failure
  }
  if (deps.metrics) {
    deps.metrics.histogram('dashboard.duration_ms', Date.now() - startedAt, {
      hasSearch: Boolean(filters?.search),
      count: summary.total,
    });
  }

  return { ok: true, value: view };
}
```

## After (Applied with structure-first)

```js
export async function buildDashboard(userId, filters, deps) {
  const contextResult = await loadDashboardContext(userId, filters, deps);
  if (!contextResult.ok) return fail(contextResult.reason);

  const selected = selectTickets(contextResult.value.tickets, contextResult.value.filters);
  const view = composeDashboardView(contextResult.value.user, selected);

  await persistDashboardCache(userId, view, deps);
  await trackDashboardViewed(userId, view.summary, contextResult.value.filters, deps);
  recordDashboardDuration(contextResult.value.startedAt, contextResult.value.filters, view.summary, deps);

  return ok(view);
}

function selectTickets(tickets, filters) {
  const filtered = applyTicketFilters(tickets, filters);
  const limited = applyTicketLimit(filtered, filters.limit);
  return sortRecentTickets(limited);
}

function composeDashboardView(user, tickets) {
  return {
    user: { id: user.id, name: user.name },
    summary: summarizeTickets(tickets),
    recent: tickets.slice(0, 5),
  };
}
```

## Interpretation

- Primary Flow: `load -> select -> compose -> cache -> track -> metrics`
- Boundary(I/O): `loadDashboardContext`, `persistDashboardCache`, `trackDashboardViewed`, `recordDashboardDuration`
- Atom(domain): `applyTicketFilters`, `applyTicketLimit`, `sortRecentTickets`, `summarizeTickets`, `composeDashboardView`
- Readability impact: filtering/sorting/summary logic is separated from external calls, reducing impact scope for UI requirement changes.
