# Perfly Agent Sync MCP

Perfly Agent Sync is a hosted MCP server for sending approved coding-agent work summaries into [Perfly](https://perfly.dev). It is built for narrow, write-only ingestion: agents can preview and submit selected summary items, but they cannot read your Perfly history, reports, profile, billing, integrations, or existing work entries.

## Endpoint

```text
https://api.perfly.dev/mcp
```

## Authentication

### OAuth

OAuth is the recommended setup for MCP clients that support server discovery and browser authorization.

Perfly publishes MCP OAuth metadata at:

```text
https://api.perfly.dev/.well-known/oauth-protected-resource/mcp
https://api.perfly.dev/.well-known/oauth-authorization-server
```

The OAuth flow uses:

- Authorization Code + PKCE
- public MCP clients
- resource-bound opaque access tokens
- rotating refresh tokens
- token revocation

### Manual Bearer Token

Use a manual bearer token only when OAuth cannot complete, such as headless CLI, SSH, devcontainer, CI, or remote sandbox environments.

Create a write-only Agent Sync token in Perfly at:

```text
https://app.perfly.dev/agent-setup
```

Then pass it as:

```text
Authorization: Bearer $PERFLY_INGESTION_TOKEN
```

Tokens start with `pfl_ing_`, are shown once, and can be revoked from the Perfly app.

## Claude Code

OAuth setup:

```bash
claude mcp add --transport http perfly https://api.perfly.dev/mcp
```

Manual token fallback:

```bash
claude mcp add --transport http perfly https://api.perfly.dev/mcp --header "Authorization: Bearer $PERFLY_INGESTION_TOKEN"
```

## Codex

OAuth-capable clients can use URL-only config:

```toml
[mcp_servers.perfly]
url = "https://api.perfly.dev/mcp"
```

Manual token fallback:

```toml
[mcp_servers.perfly]
url = "https://api.perfly.dev/mcp"
bearer_token_env_var = "PERFLY_INGESTION_TOKEN"
```

```bash
export PERFLY_INGESTION_TOKEN="pfl_ing_xxx"
```

## Cursor

OAuth-capable clients can use URL-only config:

```json
{
  "mcpServers": {
    "perfly": {
      "url": "https://api.perfly.dev/mcp"
    }
  }
}
```

Manual token fallback:

```json
{
  "mcpServers": {
    "perfly": {
      "url": "https://api.perfly.dev/mcp",
      "headers": {
        "Authorization": "Bearer $PERFLY_INGESTION_TOKEN"
      }
    }
  }
}
```

## Generic MCP Config

OAuth-capable clients:

```json
{
  "mcpServers": {
    "perfly": {
      "type": "streamable-http",
      "url": "https://api.perfly.dev/mcp"
    }
  }
}
```

Manual token fallback:

```json
{
  "mcpServers": {
    "perfly": {
      "type": "streamable-http",
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
| `perfly_check_connection` | Verify connection status without exposing secrets. |
| `perfly_get_ingestion_policy` | Return Perfly privacy and formatting rules. |
| `perfly_preview_work_items` | Validate items and preview what would be submitted without writing records. |
| `perfly_add_work_items` | Write selected summaries into Today as reviewable raw entries. |

## Submission Rules

- Preview with `perfly_preview_work_items` before writing.
- Ask for user confirmation before `perfly_add_work_items` unless unattended submission was explicitly enabled.
- Send concise summary metadata only.
- Never submit source code, diffs, logs, secrets, customer data, document bodies, issue bodies, pull request bodies, attachments, or full terminal output.

## Registry Notes

MCP registries can use this package directory or [`manifest.json`](manifest.json). The hosted server is already available at `https://api.perfly.dev/mcp`.

Smithery examples are in [`examples/smithery.md`](examples/smithery.md).

## Local Development

Localhost setup is only for contributors running the Perfly API Worker locally:

```text
http://localhost:8001/mcp
```
