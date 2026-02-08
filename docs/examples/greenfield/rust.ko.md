# Rust Greenfield Example

[Korean](rust.ko.md) | [English](rust.md)


## Prompt

```text
$structure-first 로 "문서 게시 파이프라인" 구현해줘.
- 입력: Draft
- 단계: validate -> render markdown -> save -> publish event
- 실패 reason을 enum으로 고정
```

## Example Code (핵심 발췌)

```rust
pub async fn publish_document(draft: Draft, deps: &Deps) -> Result<PublishOutput, PublishError> {
    let validated = validate_draft(&draft)?;
    let rendered = render_markdown(&validated)?;
    let saved = persist_document(&validated, &rendered, deps).await?;
    publish_document_event(&saved.document_id, deps).await?;
    Ok(saved)
}

fn validate_draft(draft: &Draft) -> Result<ValidatedDraft, PublishError> {
    if draft.title.trim().is_empty() {
        return Err(PublishError::MissingTitle);
    }
    if draft.body.trim().is_empty() {
        return Err(PublishError::MissingBody);
    }
    Ok(ValidatedDraft {
        title: draft.title.clone(),
        body: draft.body.clone(),
        tags: normalize_tags(&draft.tags),
    })
}
```

## Interpretation

- Primary Flow: `validate -> render -> persist -> publish`
- Boundaries: `persist_document`, `publish_document_event`
- Tests: `validate_draft`/`normalize_tags` 계약 검증 (로컬 계약 테스트 검증됨)
