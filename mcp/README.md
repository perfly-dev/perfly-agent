# Perfly Agent Sync MCP

Connect MCP-compatible coding agents to Perfly Agent Sync.

## Endpoint

Production:

```text
https://api.perfly.dev/mcp
```

Local development:

```text
http://localhost:8001/mcp
```

## Authentication

Create a Perfly Agent Sync token in the Perfly app at `/agent-setup`, then pass it as an HTTP authorization header:

```text
Authorization: Bearer $PERFLY_INGESTION_TOKEN
```

Tokens start with `pfl_ing_`, are shown once, and are write-only. They cannot read Perfly data.

## Claude Code

Production:

```bash
claude mcp add --transport http perfly https://api.perfly.dev/mcp --header "Authorization: Bearer $PERFLY_INGESTION_TOKEN"
```

Local development:

```bash
claude mcp add --transport http perfly-local http://localhost:8001/mcp --header "Authorization: Bearer $PERFLY_INGESTION_TOKEN"
```

## Generic MCP Config

```json
{
  "mcpServers": {
    "perfly": {
      "type": "http",
      "url": "https://api.perfly.dev/mcp",
      "headers": {
        "Authorization": "Bearer $PERFLY_INGESTION_TOKEN"
      }
    }
  }
}
```

## Tools

| Tool | Purpose |
|---|---|
| `perfly_check_connection` | Verify token status and return token metadata without exposing the secret. |
| `perfly_get_ingestion_policy` | Return Perfly's privacy and formatting rules. |
| `perfly_preview_work_items` | Validate items and preview what would be submitted without writing records. |
| `perfly_add_work_items` | Write selected summaries into Today as reviewable raw entries. |

## Submission Rules

- Preview with `perfly_preview_work_items` before writing.
- Ask for user confirmation before `perfly_add_work_items` unless unattended submission was explicitly enabled.
- Send concise summary metadata only.
- Never submit source code, diffs, logs, secrets, customer data, document bodies, issue bodies, pull request bodies, attachments, or full terminal output.
