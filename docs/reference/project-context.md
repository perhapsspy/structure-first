# Project Context

## Purpose

이 저장소는 durable 작업 맥락을 `project-context` 런타임 구조로 관리한다.
다음 세션이 다시 열렸을 때 바로 이어갈 수 있는 현재 상태는 날짜별 task에 남기고, 여러 작업에서 재사용할 규칙/배경은 reference 문서에 모은다.

## Runtime Shape

```text
docs/
  reference/**/*.md
  tasks/yyyy/mm-dd/<task-slug>/
    BRIEF.md
    logs/{DECISIONS,WORKLOG}.md
```

- `docs/reference/`는 저장소 운영 규칙, 문서 작성 경계, 반복해서 쓰는 판단 기준처럼 task를 넘어 재사용할 내용을 둔다.
- `docs/tasks/...`는 write-bearing 작업의 현재 목표, 이해 상태, 다음 단계, 검증 흔적을 남기는 기본 작업 공간으로 쓴다.
- `BRIEF.md`는 reopen/handoff용 현재 상태 문서다. append history를 밀어 넣지 말고 현재 기준으로 다시 쓴다.
- `logs/DECISIONS.md`, `logs/WORKLOG.md`만 append-only로 유지한다.

## Repo Rules

- 외부 노출 문서는 기존 원칙대로 한/영 페어를 유지한다.
- 내부 운영 문서인 `docs/reference/`, `docs/tasks/`, `docs/dogfood/README.md`와 dogfood template은 한국어를 기본으로 둔다.
- task 재사용은 파일 위치가 아니라 목표와 기대 산출물이 같은지로 판단한다.
- 목표가 달라졌거나, 성공 조건이 달라졌거나, 이해를 위해 materially different file cluster를 읽어야 했다면 새 날짜 task를 만든다.
- 애매하면 기존 task를 억지로 이어붙이지 말고 새 task를 만든 뒤 `Related Docs`로 연결한다.

## Path Rules

- 저장되는 경로는 repo-relative path 또는 `<repo-root>`, `<task-root>`, `$CODEX_HOME` 같은 안정적인 placeholder만 쓴다.
- 사용자별 절대 경로, 파일 URL, 홈 디렉터리 축약 같은 환경 종속 표기는 남기지 않는다.
- dogfood `STAGE_NOTE.md`도 같은 규칙을 따른다.

## Dogfood Boundary

- `docs/dogfood/templates/`와 playbook은 durable 운영 자산이다.
- `docs/dogfood/runs/` 아래의 `before/after`, `REVIEW`, `FEEDBACK`는 disposable 산출물이다.
- run 결과에서 반복해서 재사용할 규칙이 보이면 `docs/reference/`로 올리고, 이번 변경의 진행/결정/검증은 `docs/tasks/...`에 남긴다.
