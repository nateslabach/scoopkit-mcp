<p align="center"><img src="logo.png" width="96" alt="Scoopkit"></p>

# Scoopkit MCP server

AI-industry news for agents. When a model ships, forty outlets write about it; Scoopkit returns
the story once, as a structured event classified against a published taxonomy (10 categories,
57 subcategories), with its sources and a `correction_history` showing how the story changed.

This repo holds setup docs and an [Agent Plugins](https://agent-plugins.org) manifest (`plugin.json`, `mcp.json`), no server code. The server is hosted at **`https://api.scoopkit.dev/mcp`**
(Streamable HTTP). There is nothing to install or run.

**No API key needed to start.** Without a key you get the free tier: the last 45 days of events,
100 calls a day. A free key (same limits, tied to you) comes from
[scoopkit.dev/start](https://scoopkit.dev/start) or the `request_magic_link` tool. A Pro key adds
semantic search, a 12-month archive and 10,000 calls a day.

## Tools

| Tool | What it does | Key |
|---|---|---|
| `list_events` | Newest events first. Filter by `category`, `subcategory`, `since`, `until`; paginate with `cursor`, `limit` (max 100) | optional |
| `get_event` | One event by `event_id`, with its sources and correction history | optional |
| `taxonomy` | The category and subcategory tree, e.g. `MODEL_RELEASE`, `FUNDING_AND_DEALS` | none |
| `search` | Semantic search over events (`q`, `limit`) | Pro |
| `request_magic_link` | Emails the user a sign-in link that issues a free key (`email`) | none |

All tools except `request_magic_link` are read-only.

## Setup

### Claude (claude.ai and desktop)

Settings → Connectors → Add custom connector → URL `https://api.scoopkit.dev/mcp`.

### Claude Code

```bash
claude mcp add --transport http scoopkit https://api.scoopkit.dev/mcp
# with a key:
claude mcp add --transport http scoopkit https://api.scoopkit.dev/mcp --header "X-Api-Key: YOUR_KEY"
```

### Cursor

`~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "scoopkit": {
      "url": "https://api.scoopkit.dev/mcp"
    }
  }
}
```

### VS Code

`.vscode/mcp.json`:

```json
{
  "servers": {
    "scoopkit": {
      "type": "http",
      "url": "https://api.scoopkit.dev/mcp"
    }
  }
}
```

### Cline

`cline_mcp_settings.json`:

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

**With a key**, add `"headers": { "X-Api-Key": "YOUR_KEY" }` next to `url` in any of the JSON
configs above.

## Things to ask

- "What AI models were released this week?"
- "Show me AI funding rounds since October 1st, with sources."
- "What changed in the story about event evt_…?"

## Links

- Website: [scoopkit.dev](https://scoopkit.dev) · Get a key: [scoopkit.dev/start](https://scoopkit.dev/start)
- REST API docs: [api.scoopkit.dev/docs](https://api.scoopkit.dev/docs) · OpenAPI: [api.scoopkit.dev/openapi.json](https://api.scoopkit.dev/openapi.json)
- MCP manifest: [api.scoopkit.dev/.well-known/mcp](https://api.scoopkit.dev/.well-known/mcp)
- [Privacy](https://scoopkit.dev/privacy) · [Terms](https://scoopkit.dev/terms) · [Contact](https://scoopkit.dev/contact)
