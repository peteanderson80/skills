---
name: google-calendar
description: "Use when tasks involve Google Calendar calendars, events, scheduling, availability, or meeting management through workspace-mcp / google_workspace_mcp."
---

# Google Calendar Skill

## When to use
- List calendars, query events, or create, update, and delete calendar events.
- Use this skill when the operator has enabled Calendar access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check `CODEXCLAW_GOOGLE_WORKSPACE_MODE` and `CODEXCLAW_GOOGLE_WORKSPACE_BOUNDARY` first.
2. Use `workspace-mcp --cli <tool_name> --args '<json>'`, not fake service subcommands.
3. Prefer `get_events` for reads and `manage_event` for creates, updates, and deletes.
4. Preserve timezone information and summarize results clearly.

## Common tool names
- `list_calendars`
- `get_events`
- `manage_event`

## Example CLI usage
```
workspace-mcp --cli list_calendars --args '{}'
workspace-mcp --cli get_events --args '{"calendar_id":"primary","time_min":"2026-03-22T00:00:00Z","time_max":"2026-03-23T00:00:00Z"}'
workspace-mcp --cli manage_event --args '{"action":"create","calendar_id":"primary","summary":"Meeting","start_time":"2026-03-23T10:00:00","end_time":"2026-03-23T11:00:00"}'
```

## Notes
- Respect read-only boundaries. In read-only mode, use `list_calendars` and `get_events` only.
- Reuse `CODEXCLAW_GOOGLE_WORKSPACE_SELECTION_ARGS_JSON` instead of widening scope inside the skill.
