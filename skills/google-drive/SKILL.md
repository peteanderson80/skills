---
name: google-drive
description: "Use when tasks involve Google Drive files, folders, search, downloads, uploads, sharing, or file management through workspace-mcp / google_workspace_mcp."
---

# Google Drive Skill

## When to use
- Search Drive, inspect file content, create files or folders, or manage Drive sharing and metadata.
- Use this skill when the operator has enabled Drive access through Codexclaw's Google Workspace boundary.

## Workflow
1. Check the configured boundary first.
2. Use upstream tool names via `workspace-mcp --cli`.
3. Prefer `search_drive_files` for discovery and `get_drive_file_content` for read access.
4. Respect read-only mode before attempting file creation, copying, updates, or sharing changes.

## Common tool names
- `search_drive_files`
- `get_drive_file_content`
- `get_drive_file_download_url`
- `create_drive_file`
- `create_drive_folder`
- `import_to_google_doc`
- `get_drive_shareable_link`
- `list_drive_items`
- `copy_drive_file`
- `update_drive_file`
- `manage_drive_access`

## Example CLI usage
```
workspace-mcp --cli search_drive_files --args '{"query":"report pdf","page_size":10}'
workspace-mcp --cli get_drive_file_content --args '{"file_id":"<file-id>"}'
workspace-mcp --cli create_drive_file --args '{"name":"report.txt","content":"hello world"}'
```

## Notes
- The upstream Drive toolset also covers some Docs import and sharing workflows.
- Do not widen file access or sharing permissions beyond the configured operator boundary.
