# Python Greenfield Example

[Korean](python.ko.md) | [English](python.md)

> Note: This English text was translated and edited with LLM assistance. If anything reads awkwardly, please check the Korean version or open an issue.


## Prompt

```text
$structure-first implement a "CSV user import" feature.
- Input: csv_text
- Output: valid_rows, rejected_rows
- Return rejected reasons as fixed string values
```

## Example Code (Core Excerpt)

```python
def import_users(csv_text: str, deps):
    parsed = parse_csv_rows(csv_text)
    if not parsed["ok"]:
        return fail(parsed["reason"])

    classified = classify_rows(parsed["rows"])
    saved_count = persist_valid_users(classified["valid_rows"], deps)

    return {
        "ok": True,
        "imported": saved_count,
        "valid_rows": classified["valid_rows"],
        "rejected_rows": classified["rejected_rows"],
    }

def classify_rows(rows):
    valid_rows = []
    rejected_rows = []
    for row in rows:
        reason = validate_user_row(row)
        if reason:
            rejected_rows.append({"row": row, "reason": reason})
            continue
        valid_rows.append(normalize_user_row(row))
    return {"valid_rows": valid_rows, "rejected_rows": rejected_rows}
```

## Interpretation

- Primary Flow: `parse -> classify -> persist`
- Boundaries: `parse_csv_rows`, `persist_valid_users`
- Tests: contract table for `validate_user_row` + header/success contracts for `import_users` (verified with local contract tests)
