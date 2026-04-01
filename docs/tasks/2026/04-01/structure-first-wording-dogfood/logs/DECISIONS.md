**2026-04-01**

- 결정: wording refinement의 다음 검증은 실제 skill 추가 수정이 아니라 독립 dogfood run으로 진행한다.
- 이유: 같은 층위의 문구 루프는 이미 여러 번 돌았고, 이제는 실제 코드 산출물에서 과적용/오용이 생기는지 보는 편이 더 효율적이다.
- 대안: 예시 문서만 추가하고 run 없이 넘어가는 방안도 있었지만, wording 리스크는 stage separation이 있는 dogfood에서 더 직접 드러날 가능성이 높아 채택하지 않았다.
- 영향: 이후 skill 수정 여부는 `structure-first-wording-20260401` run evidence를 보고 판단한다.
- 결정: 이번 run의 1차 결론은 `skill wording`보다 `pipeline provenance`와 `coverage` 보강이 다음 owner라는 쪽으로 둔다.
- 이유: synthetic case 기준으로는 최근 wording refinement가 기대한 방향으로 작동했고, 더 강한 증거가 필요하다면 stage 분리와 case 확장이 우선이기 때문이다.
