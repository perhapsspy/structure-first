# Rust Greenfield Example

[Korean](rust.ko.md) | [English](rust.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


## Prompt

```text
$structure-first implement a "document publish pipeline".
- Input: Draft
- Steps: validate -> render markdown -> save -> publish event
- Fix failure reasons as enum values
```

## Example Code (Core Excerpt)

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
- Tests: contract checks for `validate_draft`/`normalize_tags` (verified with local contract tests)
