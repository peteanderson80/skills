---
name: google-calendar
description: "Use when tasks involve Google Calendar calendars, events, scheduling, availability, or meeting management through Codexclaw's wrapped Google Workspace CLI."
---

# Google Calendar Skill

## When to use
- List calendars, query events, or create, update, and delete calendar events.
- Use this skill when the operator has enabled Calendar access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check `CODEXCLAW_GOOGLE_WORKSPACE_MODE` and `CODEXCLAW_GOOGLE_WORKSPACE_BOUNDARY` first.
2. Do not call `workspace-cli` directly. Use `node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" <tool_name> key=value ...`.
3. Prefer `get_events` for reads and `manage_event` for creates, updates, and deletes.
4. Do not pass `user_google_email`; the wrapper injects the acting owner's mapped account.
4. Preserve timezone information and summarize results clearly.

## Common tool names
- `list_calendars`
- `get_events`
- `manage_event`

## Example CLI usage
```
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" list_calendars
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" get_events 'calendar_id=primary' 'time_min=2026-03-22T00:00:00Z' 'time_max=2026-03-23T00:00:00Z'
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" manage_event 'action=create' 'calendar_id=primary' 'summary=Meeting' 'start_time=2026-03-23T10:00:00' 'end_time=2026-03-23T11:00:00'
```

## Notes
- Respect read-only boundaries. In read-only mode, use `list_calendars` and `get_events` only.
- Wrapper arguments follow the real `workspace-cli call <tool> key=value ...` contract.
