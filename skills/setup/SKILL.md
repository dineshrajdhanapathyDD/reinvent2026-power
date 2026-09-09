---
name: reinvent2026-setup
description: How to install and use the re:Invent 2026 catalog MCP server bundled by this power. Use when the user asks about setting up, installing, or troubleshooting the reinvent2026 tools.
---

# re:Invent 2026 catalog — setup & usage

This power bundles the `reinvent2026-mcp` server, which exposes the AWS
re:Invent 2026 session catalog as MCP tools.

## Prerequisite (one-time)

The power launches the `reinvent2026-mcp` command, so the Python package must be
installed on the machine:

```bash
pip install reinvent2026-mcp
```

Verify it runs:

```bash
reinvent2026-mcp        # should start and wait on stdio (Ctrl+C to stop)
```

If `reinvent2026-mcp` is not on PATH, edit this power's `mcp.json` to use the
module form instead:

```json
{
  "mcpServers": {
    "reinvent2026": {
      "type": "stdio",
      "command": "python",
      "args": ["-m", "reinvent2026_mcp.server"]
    }
  }
}
```

## Tools

| Tool | Description |
|------|-------------|
| `catalog_status` | Active source + session count |
| `search_sessions` | Keyword/topic search (+ day/venue) |
| `semantic_search` | Meaning-based search from a natural-language goal |
| `get_session` | One session by id |
| `list_venues` | The six venues |
| `estimate_travel` | Walk vs. shuttle minutes between venues |
| `official_links` | Authoritative AWS re:Invent URLs |
| `refresh_catalog` | Scrape the official public catalog API (needs Playwright) |
| `load_catalog` | Load a normalized catalog JSON file |

## Example prompts

- "Search re:Invent 2026 for Amazon Bedrock chalk talks."
- "Semantic search: sessions to help me build production AI agents hands-on."
- "How far is The Venetian from MGM Grand — walk or shuttle?"
- "Give me the official re:Invent keynote and security-focus links."

## Live catalog refresh (optional)

The bundled data is the full ~1,500-session catalog. To re-scrape the latest
from the official public API:

```bash
pip install "reinvent2026-mcp[scrape]"
playwright install chromium
reinvent2026-refresh
```

## Troubleshooting

- **Server won't start**: confirm `pip show reinvent2026-mcp`; try the module
  form in `mcp.json`.
- **Empty results**: run `catalog_status` — it should report ~1,500 sessions
  from the bundled source.
- **Scrape fails**: install the `[scrape]` extra and `playwright install chromium`.
