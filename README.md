# Perfly Agent

Perfly Agent contains the public distribution artifacts for connecting coding agents to Perfly Agent Sync.

This directory is intentionally independent from Perfly's internal product docs and application source. It is safe to split or mirror into separate Git repositories for MCP registries and skill hubs.

## Packages

| Path | Purpose |
|---|---|
| `mcp/` | MCP registry package metadata, setup docs, and client examples for the hosted Perfly Agent Sync MCP endpoint. |
| `skill/` | English canonical agent skill instructions for Codex, Claude Code, and compatible coding agents. |

## Publishing

The public repository is:

```text
https://github.com/perfly-dev/perfly-agent
```

From the Perfly monorepo root, publish this directory into that repository:

```bash
pnpm publish:perfly-agent
```

Run a local split without pushing:

```bash
pnpm publish:perfly-agent -- --dry-run
```

The publish script requires a clean working tree because `git subtree split` publishes committed history only.

By default it uses the SSH remote:

```text
git@github.com:perfly-dev/perfly-agent.git
```

Override it when needed:

```bash
PERFLY_AGENT_REMOTE_URL=https://github.com/perfly-dev/perfly-agent.git pnpm publish:perfly-agent
```

If GitHub reports permission denied for an unexpected account, check the active SSH identity:

```bash
ssh -T git@github.com
```

Git commit author (`git config user.email`) does not control push permissions. SSH remotes use the GitHub account attached to the SSH key selected by your local SSH agent/config. To publish with HTTPS instead of SSH, run:

```bash
PERFLY_AGENT_REMOTE_URL=https://github.com/perfly-dev/perfly-agent.git pnpm publish:perfly-agent
```

## Hub Entries

Use one public repository with separate hub entrypoints:

- MCP registries should point to `mcp/` or `mcp/manifest.json`.
- Skill hubs should point to `skill/` or `skill/SKILL.md`.

## Privacy Boundary

Perfly Agent Sync accepts summary metadata only. Do not send source code, diffs, logs, secrets, customer data, document bodies, issue bodies, pull request bodies, attachments, or terminal output.
