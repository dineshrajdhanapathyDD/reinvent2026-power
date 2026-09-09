# reinvent2026 — Kiro Power

A **Kiro Power** that bundles the [`reinvent2026-mcp`](https://github.com/dineshrajdhanapathyDD/reinvent2026-mcp)
server so any Kiro workspace can query the **AWS re:Invent 2026** session catalog
as MCP tools — keyword **and** semantic search, venues, campus travel, and
official AWS links.

**Built by DD.** · License: **MIT**

> Not affiliated with AWS. This power *recommends*; AWS re:Invent *confirms* —
> official event info always links back to AWS.

---

## What this power does

Once installed and activated in Kiro, it gives the agent live tools to work with
the real re:Invent 2026 catalog (the full ~1,500 sessions, bundled with the
underlying package). You can ask things like:

- "Search re:Invent 2026 for Amazon Bedrock chalk talks."
- "Semantic search: sessions to help me build production AI agents hands-on."
- "How far is The Venetian from MGM Grand — walk or shuttle?"
- "Give me the official re:Invent keynote and security-focus links."

The agent calls the tools instead of guessing, and cites official AWS pages.

---

## What's inside

```
reinvent2026-power/
├── plugin.json                        # Power manifest (name, keywords, author DD, MIT)
├── mcp.json                           # Declares the stdio MCP server
├── skills/setup/SKILL.md              # Setup + usage + troubleshooting
├── dev.kiro/steering/reinvent2026.md  # Agent guidance while the power is active
├── LICENSE                            # MIT
└── README.md
```

---

## Tools

| Tool | Description |
|------|-------------|
| `catalog_status` | Active source + session count |
| `search_sessions` | Keyword/topic search (+ day/venue) |
| `semantic_search` | Meaning-based search from a natural-language goal |
| `get_session` | One session by id |
| `list_venues` | The six re:Invent venues |
| `estimate_travel` | Walk vs. shuttle minutes between venues |
| `official_links` | Authoritative AWS re:Invent URLs |
| `refresh_catalog` | Scrape the official public catalog API (needs Playwright) |
| `load_catalog` | Load a normalized catalog JSON file |

---

## Prerequisite

The power runs the `reinvent2026-mcp` command, so install the package once:

```bash
pip install reinvent2026-mcp
```

Verify it runs:

```bash
reinvent2026-mcp        # starts and waits on stdio (Ctrl+C to stop)
```

If `reinvent2026-mcp` is not on PATH, edit `mcp.json` to use the module form:

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

---

## Install the power in Kiro

1. Clone this repo:
   ```bash
   git clone https://github.com/dineshrajdhanapathyDD/reinvent2026-power.git
   ```
2. In Kiro, open the **Powers** panel → **Add Custom Power** → **Import power from a folder**.
3. Select the cloned `reinvent2026-power/` folder (the one containing `plugin.json`).
4. Trigger it by mentioning re:Invent in chat, e.g.
   *"Search re:Invent 2026 for Bedrock chalk talks."*

The MCP server activates/deactivates with the power — nothing is written into
your global `mcp.json`.

---

## Live catalog refresh (optional)

The bundled data is the full ~1,500-session catalog. To re-scrape the latest
from the official public API:

```bash
pip install "reinvent2026-mcp[scrape]"
playwright install chromium
reinvent2026-refresh
```

---

## Related

- **MCP server / package:** https://github.com/dineshrajdhanapathyDD/reinvent2026-mcp
- Install: `pip install reinvent2026-mcp`

---

## License

MIT © 2026 DD. See [LICENSE](LICENSE).

```
MIT License

Copyright (c) 2026 DD

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
