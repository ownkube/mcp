# Ownkube MCP server

The hosted [Model Context Protocol](https://modelcontextprotocol.io) server for [Ownkube](https://ownkube.io), a developer platform where a git push gives you a running app with managed Postgres and a cache beside it.

Connect it to Claude Code, Cursor, Codex or any MCP client, and you can deploy and run apps, workers, scheduled jobs, Postgres and Valkey on Ownkube from your editor or terminal.

- **Endpoint:** `https://app.ownkube.io/api/mcp` (streamable HTTP)
- **Sign-in:** OAuth in the browser, scoped to the organization you pick. Revoke access any time.
- **Registry name:** `io.ownkube/ownkube` in the [official MCP Registry](https://registry.modelcontextprotocol.io)
- **Docs:** [ownkube.io/docs/mcp](https://ownkube.io/docs/mcp) and per-client setup at [ownkube.io/agents](https://ownkube.io/agents)

This repository holds the registry metadata (`server.json`) and setup notes. The server itself is hosted, so there is nothing to install or run locally.

## What it can do

- Deploy apps, workers and cron jobs from GitHub or the Marketplace, with no AWS keys or config files
- Create and link managed Postgres databases and Valkey caches
- Read logs, metrics and deployment status, roll back a release, restart or resync a deployment
- Manage environments, variables, public hostnames, custom domains and alert rules
- Top up the wallet, set spend limits and start a plan checkout

Tools that create, change or delete infrastructure are described so your client asks you before running them. Resetting a database password and point-in-time recovery stay in the [okctl CLI](https://github.com/ownkube/ownkube-cli).

## Connect

### Claude Code

```bash
claude mcp add --transport http ownkube https://app.ownkube.io/api/mcp
```

Then run `/mcp` inside Claude Code and choose `ownkube` to sign in.

### Cursor

`~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "ownkube": {
      "url": "https://app.ownkube.io/api/mcp"
    }
  }
}
```

### VS Code (GitHub Copilot)

`.vscode/mcp.json`:

```json
{
  "servers": {
    "ownkube": {
      "type": "http",
      "url": "https://app.ownkube.io/api/mcp"
    }
  }
}
```

### Windsurf

```json
{
  "mcpServers": {
    "ownkube": {
      "serverUrl": "https://app.ownkube.io/api/mcp"
    }
  }
}
```

### Codex, Claude Desktop and other stdio clients

Bridge to the remote endpoint with [mcp-remote](https://www.npmjs.com/package/mcp-remote) (needs Node and npx):

```toml
# ~/.codex/config.toml
[mcp_servers.ownkube]
command = "npx"
args = ["-y", "mcp-remote", "https://app.ownkube.io/api/mcp"]
```

```json
{
  "mcpServers": {
    "ownkube": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://app.ownkube.io/api/mcp"]
    }
  }
}
```

The first start opens a browser tab to sign in and choose an organization.

## Pricing

Ownkube runs on a prepaid wallet, from a $5 top-up, billed per minute for what your apps use. See [ownkube.io/pricing](https://ownkube.io/pricing).

## Support

Questions and feature requests: [support@ownkube.io](mailto:support@ownkube.io) or open an issue here.

## License

The contents of this repository are [MIT](LICENSE) licensed. The Ownkube service is covered by the [Ownkube terms](https://ownkube.io/terms).
