# playground 조사 요약

## 출처

이번 문서는 `<playground>/docs/tasks/2026/06-23/codex-doc-cleanup-direction/` 작업에서 쓸만한 내용만 가져와 새 작업의 입력으로 정리한다.

원문 전체를 복사하지 않는다. 상세 근거가 필요하면 아래 문서를 다시 확인한다.

- `<playground>/docs/tasks/2026/06-23/codex-doc-cleanup-direction/DOC-CLEANUP-DIRECTION.md`
- `<playground>/docs/tasks/2026/06-23/codex-doc-cleanup-direction/RECURRING-PATTERN-INSIGHT.md`
- `<playground>/docs/tasks/2026/06-23/codex-doc-cleanup-direction/SURFACE-OWNERSHIP-PROPOSAL.md`
- `<playground>/docs/tasks/2026/06-23/codex-doc-cleanup-direction/EVIDENCE-SUMMARY.md`
- `<playground>/docs/tasks/2026/06-23/codex-doc-cleanup-direction/working/EVIDENCE-LEDGER-100.md`

## 가져갈 관찰

1. 현재 문서가 로그처럼 길어진다.
   - 현재 상태, 작업 기록, 근거, 제안이 한 문서에 섞인다.

2. 같은 표현과 이동 경로가 여러 문서에 반복된다.
   - 한 번 정한 문구가 `BRIEF.md`, 제안 문서, 근거 문서, `AGENTS.md` 후보에 다시 붙는다.

3. 기존 문구 위에 예외와 해설이 적층된다.
   - 줄여야 할 표현을 삭제하지 않고 “주의해야 한다”는 설명으로 보존한다.

4. 현재 소유 문서 확인이 늦다.
   - 이전 대화, 기억 자료, 오래된 문서가 현재 코드/API/문서 소유자보다 앞선다.

5. 근거 없는 레거시 필요를 만든다.
   - 실제 사용자 요구나 현재 소유 문서가 없는데도 레거시 독자를 상상해 내용을 늘린다.

6. 최신 지적을 방어문으로 증식한다.
   - 사용자의 정정을 실제 수정으로 처리하지 않고, 그 정정을 증명하는 설명과 중복 안내를 만든다.

7. 삭제 지시를 금지문으로 보존한다.
   - 빼라고 한 내용을 없애지 않고 “이 내용을 빼야 한다”는 문장으로 현재 문서에 남긴다.

## 가져갈 통찰

- 사용자 정정은 문서에 남길 해설 소재가 아니라 편집 입력이다.
- 이미 현재 결론을 맡은 문서가 있으면 새 설명보다 그 문서를 먼저 고쳐야 한다.
- 간결함은 문장만 짧게 쓰는 것이 아니라 한 의미가 하나의 소유 문서에만 남는 상태다.
- 삭제는 금지문 작성이 아니다. 현재 문서에서 사라지는 것이 기본 완료 조건이다.

## 버릴 것

- 새 스킬 생성 논의
- `AGENTS.md` 보강 논의
- 긴 점검표
- playground 작업의 세부 조사 과정
- 외부 참고 문헌 설명

## 다음 세션 질문

1. 후보 4줄이 기존 `Compose Rules`와 중복되지는 않는가?
2. 영어 정본 문구가 너무 추상적이면 더 자연스럽게 줄일 수 있는가?
3. 한국어 companion 문구가 한국어 문서답게 읽히는가?
4. 실제 반영 뒤 설치본 갱신까지 할지, 리포 변경만 할지 결정됐는가?
