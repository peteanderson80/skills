---
name: google-tasks
description: "Use when tasks involve Google Tasks task lists, tasks, subtasks, due dates, or task management through workspace-mcp / google_workspace_mcp."
---

# Google Tasks Skill

## When to use
- List task lists, inspect tasks, or create, update, move, and delete tasks.
- Use this skill when the operator has enabled Tasks access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check the configured boundary first.
2. Use upstream tool names with `workspace-mcp --cli`.
3. Use `manage_task` for task mutations and `manage_task_list` for list mutations.
4. Preserve task hierarchy and due dates when summarizing results.

## Common tool names
- `list_tasks`
- `get_task`
- `manage_task`
- `list_task_lists`
- `get_task_list`
- `manage_task_list`

## Example CLI usage
```
workspace-mcp --cli list_task_lists --args '{}'
workspace-mcp --cli list_tasks --args '{"task_list_id":"<task-list-id>"}'
workspace-mcp --cli manage_task --args '{"action":"create","task_list_id":"<task-list-id>","title":"New Task"}'
```

## Notes
- In read-only mode, limit yourself to `list_tasks`, `get_task`, `list_task_lists`, and `get_task_list`.
- Do not assume task-list write access unless the boundary allows it.
