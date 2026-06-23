# structure-first-docs 개선 제안

## 제안

`structure-first-docs`의 `Compose Rules`에 짧은 보강을 추가한다.

목표는 문서 작성 에이전트가 사용자 정정을 “이해했다”는 설명으로 보존하지 않고, 이미 현재 결론을 맡은 문서를 먼저 고치게 하는 것이다.

## 반영 위치

`skills/structure-first-docs/SKILL.md`에서는 아래 문장 바로 뒤가 후보 위치다.

```md
For migrations or moved ownership, make demotion explicit: old files should route to the new owner or state historical/archive status, not compete as canon.
```

`skills/structure-first-docs/SKILL.ko.md`에서도 같은 의미 위치에 한국어 문구를 맞춘다.

## 영문 후보

```md
When an existing surface owns the fact, decision, or route, change that surface before adding new prose.
Treat user corrections as edit input, not background to preserve: replace, delete, demote to archive/working, or link to the owner.
Do not add unsupported legacy-reader assumptions, defensive rationale, or duplicate routes to current documents.
Remove material marked for deletion instead of keeping prose that says to remove it.
```

## 한국어 의미 후보

```md
기존 문서가 사실·결정·이동 경로를 소유한다면, 새 설명보다 그 문서를 먼저 고친다.
사용자 정정은 보존할 배경이 아니라 편집 입력이다: 교체, 삭제, 보관·작업 문서로 격하, 또는 소유 문서로 연결.
현재 문서에는 근거 없는 레거시 독자, 방어적 해설, 중복 이동 경로를 추가하지 않는다.
삭제 대상은 “빼야 한다”는 금지문으로 남기지 말고 현재 문서에서 제거한다.
```

## 왜 이 정도만 넣는가

- 기존 스킬이 이미 소유 문서, 중복, 격하를 다룬다.
- 새 스킬이나 `AGENTS.md` 보강은 소유 영역을 늘려 같은 중복 문제를 만들 수 있다.
- 긴 체크리스트는 에이전트가 “체크했다”는 방어문을 다시 만들 위험이 있다.
- 이 보강은 새 절차가 아니라 기존 `Compose Rules`의 실패 모드를 좁히는 문구여야 한다.

## 반영 시 주의

- 실제 스킬 문구는 3-5줄 안팎으로 유지한다.
- 영어 정본과 한국어 companion의 의미를 맞춘다.
- 한국어 작업 문서에서는 식별자와 코드 블록을 제외하고 영어식 혼용을 최소화한다.
- 사용자 정정을 해설하는 문장을 새로 만들지 말고, 스킬 문구가 실제 편집 행동을 제한하는지 확인한다.

## 완료 기준

- `SKILL.md`와 `SKILL.ko.md`가 의미 동기화된다.
- 새 문구가 기존 소유 문서/격하 규칙과 경쟁하지 않는다.
- 근거 없는 레거시 독자, 방어문, 중복 이동 경로, 삭제 지시 보존을 막는 의도가 드러난다.
- `git diff --check`와 `project-context` 검사에 통과한다.
