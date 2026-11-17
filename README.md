# SingleBrain Gateway

SingleBrain Gateway is a remote MCP server. One connection reaches the marketing and sales accounts you connect yourself (Google Analytics, Search Console, HubSpot, Slack, and others) plus paid data tools that run on our accounts (such as DataForSEO, Perplexity, Exa, Apollo, and Hunter). Connected accounts are free. Paid tools are billed per call from one balance. There is no subscription, and every call is logged.

This repository is the public plugin and install shell. It is not the server source. The live server is at the address below.

[Docs](https://gateway.singlebrain.com/docs?utm_source=github_plugin&utm_medium=directory&utm_campaign=gw_distribution) · [Website](https://gateway.singlebrain.com/?utm_source=github_plugin&utm_medium=directory&utm_campaign=gw_distribution) · [Support](mailto:support@singlebrain.com)

## Install

[![Add to Cursor](https://img.shields.io/badge/Add_to-Cursor-000000?style=flat-square)](https://cursor.com/install-mcp?name=singlebrain&config=eyJ1cmwiOiJodHRwczovL2dhdGV3YXkuc2luZ2xlYnJhaW4uY29tL21jcCJ9)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=singlebrain&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fgateway.singlebrain.com%2Fmcp%22%7D)
[![Install in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install_Server-24bfa5?style=flat-square&logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=singlebrain&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fgateway.singlebrain.com%2Fmcp%22%7D&quality=insiders)

Those badges add the remote server with no key in the link. The first time the client connects, a SingleBrain page opens so you can sign in with OAuth.

## The remote address

```
https://gateway.singlebrain.com/mcp
```

Use that address as written, with no query string. The server speaks MCP over streamable HTTP. The sign-in token is issued for the plain address, and a token for an address that includes a query is refused.

Official MCP registry name (once published from the server repo): `io.github.SingleGrain-Team/singlebrain-gateway`.

## Connect with OAuth

Paste the address into a client that supports a remote MCP server. The first time it connects, a SingleBrain page opens. Sign in or create an account, pick the organization, and choose Allow. No key is copied.

### Claude (claude.ai and Claude desktop)

Open [claude.ai/customize/connectors](https://claude.ai/customize/connectors) (or Settings, Connectors in the desktop app), choose Add custom connector, paste `https://gateway.singlebrain.com/mcp`, choose Add, then choose Connect. Leave the advanced settings empty.

### Claude Code

```bash
claude mcp add --transport http singlebrain "https://gateway.singlebrain.com/mcp" --scope user
```

Then run `/mcp` in Claude Code, pick `singlebrain`, choose Authenticate, and finish sign-in on the SingleBrain page that opens.

To install this repo as a Claude Code plugin after it is on GitHub:

```bash
claude plugin marketplace add SingleGrain-Team/singlebrain-gateway-plugin
claude plugin install singlebrain-gateway@singlebrain-gateway
```

### Cursor

Click **Add to Cursor** above, or add this to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "singlebrain": {
      "url": "https://gateway.singlebrain.com/mcp"
    }
  }
}
```

A Cursor plugin manifest also lives in this repo (`.cursor-plugin/plugin.json` and root `mcp.json`) for the Cursor Marketplace and cursor.directory.

### VS Code

Click **Install in VS Code** above, or add this to `.vscode/mcp.json`:

```json
{
  "servers": {
    "singlebrain": {
      "type": "http",
      "url": "https://gateway.singlebrain.com/mcp"
    }
  }
}
```

### Codex

Add this block to `~/.codex/config.toml`. Codex defaults to OAuth for HTTP MCP servers when no bearer token is set:

```toml
[mcp_servers.singlebrain]
url = "https://gateway.singlebrain.com/mcp"
```

### Cline

This is a hosted server. Do not run a local install from the repo. In Cline, open MCP Servers, use the Remote Servers tab, and add:

- Server Name: `singlebrain`
- Server URL: `https://gateway.singlebrain.com/mcp`
- Transport Type: Streamable HTTP

If you edit the settings JSON yourself, set `"type": "streamableHttp"` on the entry. Omitting `type` makes Cline use legacy SSE. Step-by-step instructions for an agent are in [llms-install.md](./llms-install.md).

### Windsurf

Open MCP config (`mcp_config.json`) and add:

```json
{
  "mcpServers": {
    "singlebrain": {
      "serverUrl": "https://gateway.singlebrain.com/mcp"
    }
  }
}
```

Windsurf supports OAuth for Streamable HTTP remotes. Refresh the MCP plugin list after you add it.

### Goose

Goose can also install this server from the official MCP registry once it is published. To add it by hand, merge this into the `extensions` section of `~/.config/goose/config.yaml` (Windows: `%APPDATA%\Block\goose\config\config.yaml`):

```yaml
extensions:
  singlebrain:
    type: streamable_http
    name: singlebrain
    display_name: SingleBrain Gateway
    enabled: true
    uri: "https://gateway.singlebrain.com/mcp"
    timeout: 300
```

## Connect with a key

Claude Code, Codex, Cursor, and VS Code can use a key instead. Sign in, create a key in the [dashboard](https://gateway.singlebrain.com/?utm_source=github_plugin&utm_medium=directory&utm_campaign=gw_distribution), and send it on the same address as an `Authorization` header, `Bearer` followed by the key. The key acts as the member who created it. Never put a key in a chat, an email, or a command other people can read.

Cursor (`~/.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "singlebrain": {
      "url": "https://gateway.singlebrain.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_SINGLEBRAIN_KEY"
      }
    }
  }
}
```

VS Code (`.vscode/mcp.json`). VS Code will prompt for the key:

```json
{
  "inputs": [
    {
      "type": "promptString",
      "id": "singlebrain-api-key",
      "description": "SingleBrain Gateway API key",
      "password": true
    }
  ],
  "servers": {
    "singlebrain": {
      "type": "http",
      "url": "https://gateway.singlebrain.com/mcp",
      "headers": {
        "Authorization": "Bearer ${input:singlebrain-api-key}"
      }
    }
  }
}
```

Codex (`~/.codex/config.toml`). Set the environment variable to the key only. Codex sends it as `Authorization: Bearer <value>`:

```toml
[mcp_servers.singlebrain]
url = "https://gateway.singlebrain.com/mcp"
bearer_token_env_var = "SINGLEBRAIN_API_KEY"
```

Cline and Windsurf use the same `Authorization: Bearer YOUR_SINGLEBRAIN_KEY` header. See `configs/` for full examples.

Or let the device sign-in write the client entry for you:

```bash
npx -y singlebrain start --client cursor
npx -y singlebrain start --client vscode
npx -y singlebrain start --client codex
npx -y singlebrain start --client claude-code
```

It shows a code. Approve it in the browser, and it writes the server into that client. Cursor keeps it in `~/.cursor/mcp.json` under `mcpServers.singlebrain`. VS Code keeps it in `.vscode/mcp.json` and prompts for the key. Codex keeps it in `~/.codex/config.toml`.

## What's in this repo

| File | Purpose |
| --- | --- |
| `.cursor-plugin/plugin.json`, `mcp.json` | Cursor plugin (Marketplace and cursor.directory) |
| `.claude-plugin/plugin.json`, `.claude-plugin/marketplace.json`, `.mcp.json` | Claude Code plugin marketplace in this repo |
| `llms-install.md` | Agent-oriented Cline install steps |
| `assets/logo.png` | 512x512 logo |
| `assets/logo-400x400.png` | 400x400 logo for the Cline marketplace |
| `configs/` | Copy-paste snippets for Cursor, VS Code, Windsurf, Cline, Goose, and Codex |

## Help

- Docs: [gateway.singlebrain.com/docs](https://gateway.singlebrain.com/docs?utm_source=github_plugin&utm_medium=directory&utm_campaign=gw_distribution)
- Support: [support@singlebrain.com](mailto:support@singlebrain.com) or [gateway.singlebrain.com/support](https://gateway.singlebrain.com/support?utm_source=github_plugin&utm_medium=directory&utm_campaign=gw_distribution)
- Privacy: [gateway.singlebrain.com/privacy](https://gateway.singlebrain.com/privacy?utm_source=github_plugin&utm_medium=directory&utm_campaign=gw_distribution)
- Terms: [gateway.singlebrain.com/terms](https://gateway.singlebrain.com/terms?utm_source=github_plugin&utm_medium=directory&utm_campaign=gw_distribution)

## License

[MIT](./LICENSE), copyright Single Grain.
