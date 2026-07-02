# Perfly Agent

Perfly Agent connects coding assistants to [Perfly](https://perfly.dev), so approved work summaries can be written into your Perfly Today timeline without giving the agent access to your source code, issue bodies, pull requests, documents, or company SaaS accounts.

This repository contains the public agent-facing packages for Perfly Agent Sync:

| Package | Purpose |
|---|---|
| [`mcp/`](mcp/) | Hosted MCP server metadata, setup instructions, and client examples. |
| [`skill/`](skill/) | English canonical Skill instructions for Codex, Claude Code, and compatible coding agents. |

## What It Does

Perfly Agent Sync gives your coding agent a narrow write-only workflow:

1. Preview concise work summary items.
2. Ask for confirmation unless unattended submission was explicitly enabled.
3. Write selected summaries into Perfly as reviewable Today entries.

The MCP server exposes these tools:

| Tool | Purpose |
|---|---|
| `perfly_check_connection` | Verify the connection and return non-secret token/client metadata. |
| `perfly_get_ingestion_policy` | Return Perfly privacy and formatting rules. |
| `perfly_preview_work_items` | Validate items and preview what would be submitted without writing records. |
| `perfly_add_work_items` | Write selected summaries into Perfly as reviewable Today raw entries. |

## Recommended Setup

Use the hosted MCP endpoint:

```text
https://api.perfly.dev/mcp
```

Perfly supports MCP OAuth for clients that discover authorization from the server. For clients or environments that cannot complete a browser OAuth flow, Perfly also supports write-only bearer tokens created in the Perfly app.

Start with the MCP package:

- [MCP setup](mcp/)
- [Claude Code example](mcp/examples/claude-code.md)
- [Codex config example](mcp/examples/codex-config.toml)
- [Cursor config example](mcp/examples/cursor-mcp.json)

Then install or copy the Skill instructions:

- [Perfly Agent Sync Skill](skill/SKILL.md)

## Privacy Boundary

Perfly Agent Sync is designed for summary metadata only.

Do not submit:

- source code or diffs
- secrets or credentials
- customer data
- issue bodies or pull request bodies
- document bodies or attachments
- full terminal output or logs

Agents should submit short titles, optional notes, timestamps, source labels, and compact metadata references only.

## Packages And Registries

MCP registries should point to:

```text
mcp/
```

or:

```text
mcp/manifest.json
```

Skill hubs should point to:

```text
skill/
```

or:

```text
skill/SKILL.md
```

The current ClawHub listing is:

```text
https://clawhub.ai/levi840714/skills/perfly-skill
```

## Project Links

- Perfly: [https://perfly.dev](https://perfly.dev)
- App setup page: `https://app.perfly.dev/agent-setup`
- MCP endpoint: `https://api.perfly.dev/mcp`
