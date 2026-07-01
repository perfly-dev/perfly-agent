# Perfly Agent Sync Skill

This package contains the English canonical skill instructions for Perfly Agent Sync.

Use this package for skill hubs or registries. It is intentionally separate from MCP metadata because skill distribution platforms and MCP registries usually require different packaging formats.

## Entry Point

- `SKILL.md`

## Required MCP Tools

- `perfly_preview_work_items`
- `perfly_add_work_items`
- `perfly_check_connection`
- `perfly_get_ingestion_policy`

## Privacy Boundary

The skill instructs agents to submit concise work summary metadata only. It explicitly blocks source code, diffs, logs, secrets, customer data, document bodies, issue bodies, pull request bodies, attachments, and full terminal output.
