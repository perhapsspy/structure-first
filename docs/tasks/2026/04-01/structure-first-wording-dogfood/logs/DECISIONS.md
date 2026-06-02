**2026-04-01**

- **Background**: 같은 층위의 wording refinement 루프는 이미 여러 번 돌았고, 이제는 실제 코드 산출물에서 과적용/오용이 생기는지 보는 검증이 더 효율적인 상태였다.
- **Decision**: 다음 검증은 skill 추가 수정이 아니라 독립 `structure-first-wording-20260401` dogfood run으로 진행하고, 1차 결론은 `skill wording`보다 `pipeline provenance`와 `coverage` 보강이 다음 owner라는 쪽으로 둔다.
- **Why**: wording 리스크는 stage separation이 있는 dogfood에서 더 직접 드러날 가능성이 높고, synthetic case 기준으로는 최근 wording refinement가 기대한 방향으로 작동했기 때문이다.
- **Impact**: 이후 skill 수정 여부는 dogfood run evidence를 보고 판단하며, 더 강한 증거가 필요하면 stage 분리와 case 확장을 우선한다.
