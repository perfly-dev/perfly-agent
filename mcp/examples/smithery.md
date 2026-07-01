# Smithery Publishing Notes

Perfly Agent Sync is a hosted Streamable HTTP MCP server:

```text
https://api.perfly.dev/mcp
```

Publish the URL-based server:

```bash
smithery auth login
smithery mcp publish "https://api.perfly.dev/mcp" -n perfly-dev/perfly-agent
```

Perfly currently requires a write-only ingestion token in the upstream `Authorization` header:

```text
Authorization: Bearer pfl_ing_xxx
```

If Smithery requires a config schema for auth-required scanning or user setup, use a user-facing header that is not named `Authorization`, then forward it to upstream `Authorization` with Smithery's `x-to` mapping:

```json
{
  "type": "object",
  "properties": {
    "perflyAuthorization": {
      "type": "string",
      "title": "Perfly Authorization header",
      "description": "Use the full value: Bearer pfl_ing_xxx",
      "x-from": { "header": "x-perfly-authorization" },
      "x-to": { "header": "Authorization" }
    }
  },
  "required": ["perflyAuthorization"]
}
```

This avoids using `Authorization` as the incoming `x-from` header, which Smithery reserves for its own OAuth flow, while still sending the value as `Authorization` to Perfly.

Long-term, OAuth 2.1 support would make hosted registry onboarding cleaner for GUI clients.
