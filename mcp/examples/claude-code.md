# Claude Code MCP Setup

Create a Perfly Agent Sync token in the Perfly app at `/agent-setup`, store it outside chat, then run:

```bash
export PERFLY_INGESTION_TOKEN="pfl_ing_xxx"
claude mcp add --transport http perfly https://api.perfly.dev/mcp --header "Authorization: Bearer $PERFLY_INGESTION_TOKEN"
```

For local development while the API Worker is running on port `8001`:

```bash
claude mcp add --transport http perfly-local http://localhost:8001/mcp --header "Authorization: Bearer $PERFLY_INGESTION_TOKEN"
```
