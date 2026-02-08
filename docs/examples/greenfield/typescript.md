# TypeScript Greenfield Example

[Korean](typescript.ko.md) | [English](typescript.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


## Prompt

```text
$structure-first implement a "notification priority queue" logic.
- Input: NotificationRequest[]
- Output: queue (sorted), dropped (with reason)
- Rule: exclude quiet hour, higher severity first, then older createdAt
```

## Example Code (Core Excerpt)

```ts
export function buildNotificationQueue(input: unknown): BuildQueueResult {
  const parsed = parseNotificationRequests(input);
  if (!parsed.ok) return { ok: false, reason: 'invalid_input' };

  const split = splitDeliverable(parsed.value);
  const queue = sortByPriority(split.deliverable);

  return { ok: true, queue, dropped: split.dropped };
}

function splitDeliverable(requests: NotificationRequest[]) {
  const deliverable: NotificationRequest[] = [];
  const dropped: DroppedNotification[] = [];

  for (const req of requests) {
    const reason = validateNotification(req);
    if (reason) dropped.push({ request: req, reason });
    else deliverable.push(req);
  }

  return { deliverable, dropped };
}

function validateNotification(req: NotificationRequest): 'quiet_hour' | 'invalid_shape' | null {
  if (!req || !req.id || !req.userId) return 'invalid_shape';
  if (!Number.isFinite(req.severity) || !Number.isFinite(req.createdAt)) return 'invalid_shape';
  if (typeof req.quietHour !== 'boolean') return 'invalid_shape';
  if (req.quietHour) return 'quiet_hour';
  return null;
}
```

## Interpretation

- Primary Flow: `parse -> split -> sort`
- Boundaries: `parseNotificationRequests`
- Tests: shape/quiet-hour contracts (`validateNotification`) + priority sorting contract (`sortByPriority`) (verified with local contract tests)
