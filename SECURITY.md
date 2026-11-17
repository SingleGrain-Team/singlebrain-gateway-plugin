# Security

SingleBrain Gateway is a hosted MCP server. This repository only contains plugin manifests, install snippets, and logos. It does not include server source code or secrets.

## Report a vulnerability

Email [support@singlebrain.com](mailto:support@singlebrain.com). Do not open a public issue for a vulnerability, a leaked key, or anything that could let someone else use an account.

## Keys

If a Gateway key was exposed, revoke it in the [dashboard](https://gateway.singlebrain.com) and create a new one. A revoked key stops working at once.

Never put a key in a chat, an email, a command other people can read, or a commit in this repo. The example configs use placeholders only.

## The remote address

The MCP endpoint is `https://gateway.singlebrain.com/mcp`. Use it with no query string. A query string changes the OAuth audience, and a token issued for the plain address is then refused.
