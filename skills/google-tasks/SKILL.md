---
name: google-tasks
description: "Use when tasks involve Google Tasks task lists, tasks, subtasks, due dates, or task management through Codexclaw's wrapped Google Workspace CLI."
---

# Google Tasks Skill

## When to use
- List task lists, inspect tasks, or create, update, move, and delete tasks.
- Use this skill when the operator has enabled Tasks access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check the configured boundary first.
2. Do not call `workspace-cli` directly. Use `node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" <tool_name> key=value ...`.
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
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" list_task_lists
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" list_tasks 'task_list_id=<task-list-id>'
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" manage_task 'action=create' 'task_list_id=<task-list-id>' 'title=New Task'
```

## Notes
- In read-only mode, limit yourself to `list_tasks`, `get_task`, `list_task_lists`, and `get_task_list`.
- Do not pass `user_google_email`; the wrapper injects it.
- Do not assume task-list write access unless the boundary allows it.
