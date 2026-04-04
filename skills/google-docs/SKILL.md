---
name: google-docs
description: "Use when tasks involve Google Docs documents, document text, markdown export, find/replace, formatting, or comments through Codexclaw's wrapped Google Workspace CLI."
---

# Google Docs Skill

## When to use
- Read Docs content, create documents, modify text, export to markdown, or manage comments.
- Use this skill when the operator has enabled Docs access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check the configured Google Workspace boundary first.
2. Do not call `workspace-cli` directly. Use `node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" <tool_name> key=value ...`.
3. Prefer `get_doc_content` or `get_doc_as_markdown` for reads, and `modify_doc_text` for text edits.
4. Respect read-only mode and avoid create or modify tools when writes are not allowed.

## Common tool names
- `search_docs`
- `get_doc_content`
- `create_doc`
- `modify_doc_text`
- `find_and_replace_doc`
- `list_docs_in_folder`
- `insert_doc_elements`
- `update_paragraph_style`
- `get_doc_as_markdown`
- `export_doc_to_pdf`
- `list_document_comments`
- `manage_document_comment`

## Example CLI usage
```
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" search_docs 'query=project plan' page_size=10
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" get_doc_content 'document_id=<document-id>'
node "$CODEXCLAW_GOOGLE_WORKSPACE_WRAPPER_SCRIPT" modify_doc_text 'document_id=<document-id>' 'action=append' 'text=Hello, world!'
```

## Notes
- Some Docs operations use both Docs and Drive scopes upstream. Stay within the configured operator boundary.
- Do not pass `user_google_email`; the wrapper injects it.
- Prefer markdown export when the user needs the document content as reusable text.
