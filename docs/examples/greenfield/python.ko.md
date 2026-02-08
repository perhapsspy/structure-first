# Python Greenfield Example

[Korean](python.ko.md) | [English](python.md)


## Prompt

```text
$structure-first 를 사용해서 "CSV 사용자 업로드" 기능 구현해줘.
- 입력: csv_text
- 출력: valid_rows, rejected_rows
- rejected 사유를 고정 문자열로 반환
```

## Example Code (핵심 발췌)

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
- Tests: `validate_user_row` 계약 테이블 + `import_users` 헤더/성공 계약 검증 (로컬 계약 테스트 검증됨)
