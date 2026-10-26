# Installing the Scoopkit MCP server

Scoopkit is a hosted remote MCP server. Do not clone, build or run anything.

1. Add this server to the MCP settings file:

```json
{
  "mcpServers": {
    "scoopkit": {
      "type": "streamableHttp",
      "url": "https://api.scoopkit.dev/mcp"
    }
  }
}
```

2. No API key is required. Without one, `list_events`, `get_event` and `taxonomy` work at the
   free tier (last 45 days, 100 calls a day). Only `search` needs a key (Pro).

3. If the user wants a key, call the `request_magic_link` tool with their email address. They
   click the link in the email and paste the key back. Then add it to the server entry:

```json
"headers": { "X-Api-Key": "THE_KEY" }
```

4. To check it works, call `taxonomy` (no arguments), then `list_events` with `{"limit": 3}`.
