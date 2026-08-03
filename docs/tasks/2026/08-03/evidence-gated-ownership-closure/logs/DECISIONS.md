**2026-08-03**
- current unit 국소 검증은 실제 actor·외부 schema·mutation 경계의 closure 누락을 놓칠 수 있지만 무조건 재귀는 과잉 분해와 토큰 비용을 만든다.
- automatic recursive descent와 Goal/Codex 결합은 제외하고, evidence-triggered bounded closure와 가장 가까운 real-contract witness를 우선 후보로 평가한다.
- 최근 positive 사례는 evidence 기반 재평가가 구조를 개선했고, negative 사례는 helper/unit 검증만으로 실제 계약을 닫았다고 간주한 지점에서 실패했다.
- Phase 1은 Pro의 반박 가능한 판단과 A/B/C 후보 비교까지만 수행하며 정본 수정은 상위 director follow-up 뒤에 연다.

**2026-08-03**
- 현재 line 18/24/33-44는 owner 범주를 충분히 다루지만 line 20의 stay-local 조건을 authoritative evidence가 반증할 때 current-unit 선택을 다시 여는 규칙은 명시하지 않는다.
- 최소 core 후보는 line 20에서 contradictory evidence가 가장 작은 새 implicated unit만 reopen하게 하고, line 40에서 material actor/schema/write/effect claim의 nearest safe owner-sourced witness를 요구하며, line 44에서 witness 불가 시 unresolved boundary와 exact next check를 남기는 A로 둔다.
- 이 안은 2b68ad9에서 제거한 generic final gate를 복원하지 않고 9165d05의 압축성을 유지하면서 DI-1850 positive control은 추가 extraction 없이 멈추고 Fielder negative control은 premature closure를 막는다.
- 상위 director 승인 전에는 SKILL 한·영 pair, dogfood, README를 수정하지 않으며 Phase 2에서 A/B/C forward-test 범위를 결정한다.

**2026-08-03**
- 기존 stay-local 문장은 focused verification의 통과만으로 current-unit owner 가정을 고정할 수 있고, local tests가 material 외부 경계의 closure evidence로 과대 해석될 수 있다.
- focused verification이 ownership과 completion meaning을 지지할 때만 stay-local하고, 다른 owner 증거가 나오면 가장 작은 새 implicated unit 하나만 다시 열며, material boundary claim은 boundary-owned nearest safe representative witness로 검증한다.
- 이 규칙은 generic final gate나 recursive descent 없이 Fielder형 premature closure를 막고, production·full end-to-end를 자동 요구하지 않아 DI-1850형 닫힌 owner에서 추가 구조화를 피한다.
- safe witness를 실행·확인할 수 없으면 boundary를 unresolved로 남기고 exact next check·responsible unit·required cases를 밝히며 local tests만으로 closure를 주장하지 않는다. 다음 채택 gate는 독립 forward-test다.

**2026-08-03**
- 최종 wording과 forward-test가 승인됐고 독립 리뷰에서 열린 finding이 없으며 사용자가 배포를 명시 승인했다.
- 현재 변경을 structure-first의 trigger와 제품 역할을 바꾸지 않는 core-contract patch로 canonical main에 publish한다.
- 변경은 기존 owner 탐색 능력에 새 workflow를 추가하지 않고 premature closure 방지 계약만 선명하게 하며 frontmatter와 공개 trigger surface를 유지한다.
- Canonical commit은 Project Legibility 0.7.1 patch handoff의 source가 되며 release, tag, downstream sync는 별도 owner에 남긴다.
