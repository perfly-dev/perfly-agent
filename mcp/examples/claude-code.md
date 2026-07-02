# Claude Code MCP Setup

OAuth setup:

```bash
claude mcp add --transport http perfly https://api.perfly.dev/mcp
```

Claude Code should open the Perfly MCP OAuth authorization flow. After approval, it receives resource-bound MCP credentials for the hosted endpoint.

Manual token fallback:

```bash
export PERFLY_INGESTION_TOKEN="pfl_ing_xxx"
claude mcp add --transport http perfly https://api.perfly.dev/mcp --header "Authorization: Bearer $PERFLY_INGESTION_TOKEN"
```

Use the fallback only when OAuth cannot complete, such as headless, SSH, devcontainer, CI, or remote sandbox workflows.
