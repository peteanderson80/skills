---
name: google-slides
description: "Use when tasks involve Google Slides presentations, slide creation, slide updates, thumbnails, or presentation comments through workspace-mcp / google_workspace_mcp."
---

# Google Slides Skill

## When to use
- Create presentations, inspect slide content, apply batch updates, or work with slide comments.
- Use this skill when the operator has enabled Slides access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check the configured Google Workspace boundary first.
2. Use upstream tool names via `workspace-mcp --cli`.
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
workspace-mcp --cli get_presentation --args '{"presentation_id":"<presentation-id>"}'
workspace-mcp --cli get_page --args '{"presentation_id":"<presentation-id>","page_object_id":"<page-id>"}'
workspace-mcp --cli create_presentation --args '{"title":"Quarterly Review"}'
```

## Notes
- Complex slide edits usually go through `batch_update_presentation`, not a simple write subcommand.
- Stay within the configured service, tier, and read-only boundary.
