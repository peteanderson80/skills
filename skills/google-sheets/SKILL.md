---
name: google-sheets
description: "Use when tasks involve Google Sheets spreadsheets, ranges, cells, formatting, spreadsheet creation, or analysis through Codexclaw's wrapped Google Workspace CLI."
---

# Google Sheets Skill

## When to use
- Read or modify sheet values, inspect spreadsheet metadata, create spreadsheets, or format ranges.
- Use this skill when the operator has enabled Sheets access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check `CODEXCLAW_GOOGLE_WORKSPACE_MODE` and `CODEXCLAW_GOOGLE_WORKSPACE_BOUNDARY` first.
2. Do not call `workspace-cli` directly. Use `node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" <tool_name> key=value ...`.
3. Prefer narrow range reads and writes instead of oversized sheet operations.
4. Respect read-only mode and avoid value or formatting mutations when writes are not allowed.

## Common tool names
- `list_spreadsheets`
- `read_sheet_values`
- `modify_sheet_values`
- `create_spreadsheet`
- `get_spreadsheet_info`
- `format_sheet_range`
- `create_sheet`
- `list_spreadsheet_comments`
- `manage_spreadsheet_comment`
- `manage_conditional_formatting`

## Example CLI usage
```
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" list_spreadsheets max_results=10
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" read_sheet_values 'spreadsheet_id=<spreadsheet-id>' 'range=Sheet1!A1:C10'
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" modify_sheet_values 'action=update' 'spreadsheet_id=<spreadsheet-id>' 'range=Sheet1!A1:C1' 'values=[["foo","bar","baz"]]'
```

## Notes
- `list_spreadsheets` uses Drive-backed discovery; that is normal for this upstream project.
- Do not pass `user_google_email`; the wrapper injects it.
