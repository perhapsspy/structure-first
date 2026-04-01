**2026-04-01**

- 결정: 기존 dogfood run은 provenance가 약하므로 덮어쓰지 않고, playbook/template를 강화한 뒤 새 rerun으로 다시 검증한다.
- 이유: 문제의 owner가 `skill wording`이 아니라 `pipeline + execution discipline`일 가능성이 높고, 기존 artifact는 그 사실 자체를 증거로 보관할 가치가 있다.
- 대안: 기존 run만 수정하는 방안도 있었지만, history가 섞여 provenance 실패 원인을 흐리게 만들어 채택하지 않았다.
- 영향: 이후 dogfood 결과 해석에서는 기존 run을 negative evidence, rerun을 corrected evidence로 비교할 수 있다.
