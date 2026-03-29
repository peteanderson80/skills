---
name: gmail
description: "Use when tasks involve Gmail email, inbox search, reading messages, sending email, drafts, labels, or filters through workspace-mcp / google_workspace_mcp."
---

# Gmail Skill

## When to use
- Search Gmail, read messages or threads, send email, create drafts, or manage labels.
- Use this skill when the operator has enabled Gmail access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check `CODEXCLAW_GOOGLE_WORKSPACE_MODE` and `CODEXCLAW_GOOGLE_WORKSPACE_BOUNDARY` first.
2. If Google Workspace integration is disabled, do not pretend Gmail tools are available.
3. In Codexclaw, prefer the CLI path using `CODEXCLAW_GOOGLE_WORKSPACE_CLI_BIN` and `CODEXCLAW_GOOGLE_WORKSPACE_SELECTION_ARGS_JSON`.
4. Call upstream tool names via `workspace-mcp --cli <tool_name> --args '<json>'`.
5. Use the narrowest tool that solves the task and keep requests within the configured boundary.
6. Summarize important results for the user instead of dumping raw JSON unless the task calls for machine-readable output.

## Common tool names
- `search_gmail_messages`
- `get_gmail_message_content`
- `get_gmail_messages_content_batch`
- `send_gmail_message`
- `get_gmail_thread_content`
- `draft_gmail_message`
- `list_gmail_labels`
- `manage_gmail_label`
- `modify_gmail_message_labels`
- `manage_gmail_filter`

## Example CLI usage
```
workspace-mcp --cli search_gmail_messages --args '{"query":"from:someone@example.com","max_results":10}'
workspace-mcp --cli get_gmail_message_content --args '{"message_id":"<message-id>"}'
workspace-mcp --cli send_gmail_message --args '{"to":["user@example.com"],"subject":"Hello","body":"Hi there!"}'
```

## Notes
- The old `google_workspace_mcp gmail ...` subcommand shape is not correct for the upstream project.
- Reuse `CODEXCLAW_GOOGLE_WORKSPACE_SELECTION_ARGS_JSON` when you need the operator-defined service or permission boundary.
- Respect read-only mode. If the configured boundary is read-only, do not attempt send, draft, label, or filter mutations.

## Boundary reminder
- Operator-defined boundary metadata is available in `CODEXCLAW_GOOGLE_WORKSPACE_MODE`, `CODEXCLAW_GOOGLE_WORKSPACE_CLI_BIN`, `CODEXCLAW_GOOGLE_WORKSPACE_SELECTION_ARGS_JSON`, and `CODEXCLAW_GOOGLE_WORKSPACE_BOUNDARY`.
- Never assume Gmail write access just because the upstream tool supports it.
