---
name: google-slides
description: "Use when tasks involve Google Slides presentations, slide creation, slide updates, thumbnails, or comments through Codexclaw's wrapped Google Workspace CLI."
---

# Google Slides Skill

## When to use
- Create presentations, inspect slide content, apply batch updates, or work with slide comments.
- Use this skill when the operator has enabled Slides access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check the configured Google Workspace boundary first.
2. Do not call `workspace-cli` directly. Use `node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" <tool_name> key=value ...`.
3. Use `get_presentation` or `get_page` for reads and `batch_update_presentation` for structural edits.
4. Respect read-only mode and avoid create or update tools when writes are not allowed.

## Common tool names
- `create_presentation`
- `get_presentation`
- `batch_update_presentation`
- `get_page`
- `get_page_thumbnail`
- `list_presentation_comments`
- `manage_presentation_comment`

## Example CLI usage
```
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" get_presentation 'presentation_id=<presentation-id>'
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" get_page 'presentation_id=<presentation-id>' 'page_object_id=<page-id>'
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" create_presentation 'title=Quarterly Review'
```

## Notes
- Complex slide edits usually go through `batch_update_presentation`, not a simple write subcommand.
- Do not pass `user_google_email`; the wrapper injects it.
- Stay within the configured service, tier, and read-only boundary.
