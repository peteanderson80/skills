---
name: gmail
description: "Use when tasks involve Gmail email, inbox search, reading messages, sending email, drafts, labels, or filters through Codexclaw's wrapped Google Workspace CLI."
---

# Gmail Skill

## When to use
- Search Gmail, read messages or threads, send email, create drafts, or manage labels.
- Use this skill when the operator has enabled Gmail access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check `CODEXCLAW_GOOGLE_WORKSPACE_MODE` and `CODEXCLAW_GOOGLE_WORKSPACE_BOUNDARY` first.
2. If Google Workspace integration is disabled, do not pretend Gmail tools are available.
3. In Codexclaw, do not call `workspace-cli` directly. Use `node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" <tool_name> key=value ...`.
4. Do not pass `user_google_email`; the wrapper injects the acting owner's mapped account.
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
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" search_gmail_messages 'query=from:someone@example.com' max_results=10
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" get_gmail_message_content 'message_id=<message-id>'
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" send_gmail_message 'to=["user@example.com"]' 'subject=Hello' 'body=Hi there!'
```

## Notes
- The old `workspace-mcp --cli ... --args '{...}'` shape is not correct for this setup.
- Wrapper arguments follow the real `workspace-cli call <tool> key=value ...` contract, so arrays or objects must be JSON-encoded inside a single `key=...` argument.
- Respect read-only mode. If the configured boundary is read-only, do not attempt send, draft, label, or filter mutations.

## Boundary reminder
- Operator-defined boundary metadata is available in `CODEXCLAW_GOOGLE_WORKSPACE_MODE`, `CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT`, `CODEXCLAW_GOOGLE_WORKSPACE_MCP_ENDPOINT`, and `CODEXCLAW_GOOGLE_WORKSPACE_BOUNDARY`.
- Never assume Gmail write access just because the upstream tool supports it.
