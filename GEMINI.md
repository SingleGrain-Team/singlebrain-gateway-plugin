# SingleBrain Gateway

This extension connects Gemini CLI to SingleBrain Gateway, a remote MCP server at `https://gateway.singlebrain.com/mcp`. It reaches the marketing and sales accounts the user connects (such as Google Analytics, Search Console, HubSpot, and Slack) and paid data tools billed per call from one balance.

- On first use, run `/mcp auth singlebrain` to sign in with OAuth in the browser.
- Connected accounts are free. Paid tools are billed per call, and every call is logged.
- If OAuth is not an option, create an API key in the Gateway dashboard and send it as an `Authorization: Bearer <key>` header instead.
- Use the plain address with no query string.
