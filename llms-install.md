# Install SingleBrain Gateway in Cline

This is a remote MCP server. Do not clone this repository to run a local process. Do not run npm, pip, or docker. Cline only needs the hosted URL below.

The server address is:

```
https://gateway.singlebrain.com/mcp
```

Use that address exactly, with no query string.

## Prerequisites

- Cline (the IDE extension or the Cline CLI)
- A SingleBrain Gateway account, created during sign-in, or an existing API key from the dashboard at https://gateway.singlebrain.com

## Step 1: Open Cline MCP settings

In the Cline panel, click the MCP Servers icon, open the Configure tab, and choose Configure MCP Servers. That opens the MCP settings JSON.

The CLI stores the same file at `~/.cline/data/settings/cline_mcp_settings.json` unless `CLINE_MCP_SETTINGS_PATH` is set. You can also run `cline mcp` and choose Add server.

## Step 2: Add the remote server (OAuth, preferred)

If you are using the Remote Servers tab: set Server Name to `singlebrain`, Server URL to `https://gateway.singlebrain.com/mcp`, choose Transport Type Streamable HTTP, and click Add Server.

If you are editing the JSON, add this entry under `mcpServers`. The `type` field must be `streamableHttp`. If you omit `type`, Cline defaults to legacy SSE, which this server does not use.

```json
{
  "mcpServers": {
    "singlebrain": {
      "type": "streamableHttp",
      "url": "https://gateway.singlebrain.com/mcp",
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Save the file.

## Step 3: Sign in

The first time Cline connects, a SingleBrain page should open. Sign in or create an account, pick the organization, and choose Allow. No key is copied.

If you are using the Cline CLI, you can start or retry that sign-in with `cline mcp` and the Authorize OAuth action.

## Alternative: connect with a key

If OAuth sign-in cannot finish, create a key in the dashboard and send it as an `Authorization` header, `Bearer` followed by the key. Never put the key in a chat or a commit.

```json
{
  "mcpServers": {
    "singlebrain": {
      "type": "streamableHttp",
      "url": "https://gateway.singlebrain.com/mcp",
      "headers": {
        "Authorization": "Bearer YOUR_SINGLEBRAIN_KEY"
      },
      "disabled": false,
      "autoApprove": []
    }
  }
}
```

Replace `YOUR_SINGLEBRAIN_KEY` with the key. The key acts as the member who created it.

The Cline CLI can add the same server with:

```bash
cline mcp add singlebrain https://gateway.singlebrain.com/mcp --transport http --header "Authorization: Bearer YOUR_SINGLEBRAIN_KEY" --yes
```

## Step 4: Verify

Enable the `singlebrain` server if it is disabled. Confirm it is connected and that tools appear. Ask Cline a small question that would use the account tools, such as listing what SingleBrain can reach. If the server fails to start, check that the URL has no query string, that `type` is `streamableHttp`, and that sign-in finished or the `Authorization` header is present and correct.

## Troubleshooting

- Connection or 401 errors: finish OAuth sign-in, or check the key and the `Authorization: Bearer` header.
- No tools: make sure the server is enabled and restart it from MCP settings.
- Wrong transport: if `type` is missing, Cline uses SSE. Set `"type": "streamableHttp"`.
- Help: support@singlebrain.com
