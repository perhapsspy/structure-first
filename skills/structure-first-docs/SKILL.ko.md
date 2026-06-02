# Skill: Structure First Docs (Korean Companion)

> Review-only Korean companion. Canonical skill file: `SKILL.md`.

## Purpose

엔지니어링 문서와 문서 패키지를 읽기 쉽고, 재개하기 쉽고, 코드 작업의 기반으로 쓰기 좋게 만든다.

큰 작업의 문서 세트는 코드 패키지처럼 본다. 명확한 entrypoint, 단일 책임 module, reader route, 현재 source of truth/증거/기록/초안/낡은 자료 분리가 핵심이다.

## Modes

- **Document Compose**: 문서 하나 작성/재구성
- **Document Review**: 문서 하나 리뷰, 이슈/리스크 우선
- **Package Compose**: 여러 파일로 된 설계/마이그레이션/런북/구현/인계 패키지 구성
- **Package Review**: 패키지의 소유권, navigation, stale state, 중복, 구현 준비도 리뷰

## Principles

- path, filename, log, archive, work area는 기존 프로젝트 관례를 따른다. 이 스킬은 저장 구조가 아니라 의미 구조를 판단한다.
- 원문 의미를 보존한다. 사실, 약속, 담당, 날짜, 수치, 제약, 결정을 새로 만들지 않는다.
- 추정은 추정으로 둔다. 가능성, 의심, 선택지를 결정으로 바꾸지 않는다.
- 현재 source of truth를 증거, chronology, 초안, archive와 분리한다.
- 현재 결정, 계약, gate, 계획 하나에는 owning document 하나만 둔다.
- package entry 문서는 보통 current canon, router, bounded execution/runbook packet 중 하나여야 한다.
- 이메일, 체크리스트, ADR, 런북, 인계, 로그처럼 유용한 원문 양식은 유지한다.
- 구조 개선 효과가 작으면 no-op나 light-touch edit를 우선한다.
- 리뷰는 문서 상태, 소유권, 범위, 리스크를 명확히 한다. 원문이 이미 다루지 않는 시스템 재설계로 번지지 않는다.

## Package Roles

고정 템플릿이 아니라 lens로 쓴다.

- **Entrypoint**: 패키지 목적, 현재 상태, 시작점을 말한다.
- **Router**: reader goal을 문서와 파일 책임에 연결한다.
- **Canonical module**: 현재 topic, contract, model, decision, plan 하나를 소유한다.
- **Gate/runbook**: precondition, allowed action, stop condition, owner/approval boundary, evidence, rollback, recovery를 소유한다.
- **Backlog/TODO**: live checklist, deletion-style TODO, historical audit 중 성격을 명확히 한다.
- **Evidence/log**: 증거와 chronology를 보존하되 current canon처럼 보이지 않게 한다.
- **Working/archive**: 미확정 또는 stale material을 현재 문서와 분리한다.
- **Reference candidate**: durable reference로 승격할 만한 reusable current context를 담는다.

## Compose Rules

고정 템플릿보다 reader job에서 시작한다.

- **Resume**: 지금 무엇이 참이고, 다음은 무엇이며, 무엇이 막혔는가?
- **Decide**: 어떤 사실, 선택지, tradeoff, open question이 중요한가?
- **Implement**: 어떤 계약, 경계, 순서, acceptance criteria가 코드 작업을 이끄는가?
- **Verify**: 어떤 gate, command, scenario, evidence가 작업을 닫는가?
- **Operate**: 어떤 runbook, rollback, owner, stop condition이 중요한가?

원문이 정당화하는 surface만 만든다. 두 문서가 같은 현재 결론을 반복하면 source나 기존 관례상 ownership이 명확할 때만 하나를 owner로 정하고, 그렇지 않으면 ownership decision으로 표시한다.

ownership이 이동한 경우 예전 파일은 새 owner로 routing하거나 historical/archive status를 명시해야 하며, canon처럼 경쟁하면 안 된다.

## Review Rules

`Issues/Risks`를 심각도 순으로 먼저 제시하고, 그다음 evidence와 required changes를 쓴다.

확인할 것:

- entrypoint가 없거나 오해를 만든다
- resume, decision, implementation, verification, operation reader path가 불명확하다
- 같은 현재 결정, 계약, gate, 계획에 owner가 둘 이상이다
- 초안, evidence dump, stale report가 current처럼 보인다
- current summary에 chronology나 command transcript가 섞였다
- log나 research 안에만 현재 결론이 있다
- backlog style이 모호하거나 open/completed/deployment/validation/staging material이 섞였다
- gate/runbook에 precondition, stop condition, rollback, recovery, evidence, approval boundary가 빠졌다
- ownership 이동 뒤에도 예전 파일이 canonical처럼 보인다
- stale/archive 링크에 status label이 없다
- canonical-vs-router, reference promotion, archive retention, backlog style처럼 명시적인 ownership 또는 policy choice가 필요한 결정이 숨어 있다

source에서 정해지지 않은 ownership 또는 policy choice가 필요한 변경은 조용히 rewrite하지 말고 decision request로 표시한다.
append-only log는 깔끔하게 만들기 위해 다시 쓰지 않는다. historical cleanup 요청이 없으면 관련 tail만 sample한다.

## Output Contract

Compose는 가능하면 직접 수정한다. 막히면 publish-ready Markdown과 blocked input을 반환한다.

Review는 아래 형태를 쓴다.

```text
Issues/Risks
Evidence
Required Changes
Open Questions or Decision Requests
```
