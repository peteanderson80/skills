---
name: google-sheets
description: "Use when tasks involve Google Sheets spreadsheets, ranges, cells, formatting, spreadsheet creation, or analysis through workspace-mcp / google_workspace_mcp."
---

# Google Sheets Skill

## When to use
- Read or modify sheet values, inspect spreadsheet metadata, create spreadsheets, or format ranges.
- Use this skill when the operator has enabled Sheets access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check `CODEXCLAW_GOOGLE_WORKSPACE_MODE` and `CODEXCLAW_GOOGLE_WORKSPACE_BOUNDARY` first.
2. Use upstream tool names via `workspace-mcp --cli ...`.
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
workspace-mcp --cli list_spreadsheets --args '{"max_results":10}'
workspace-mcp --cli read_sheet_values --args '{"spreadsheet_id":"<spreadsheet-id>","range":"Sheet1!A1:C10"}'
workspace-mcp --cli modify_sheet_values --args '{"action":"update","spreadsheet_id":"<spreadsheet-id>","range":"Sheet1!A1:C1","values":[["foo","bar","baz"]]}'
```

## Notes
- `list_spreadsheets` uses Drive-backed discovery; that is normal for this upstream project.
- Reuse the operator-defined selection args instead of choosing broader services inside the skill.
