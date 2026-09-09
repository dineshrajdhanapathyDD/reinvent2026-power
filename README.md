# reinvent2026 — Kiro Power

A **Kiro Power** that bundles the [`reinvent2026-mcp`](https://github.com/dineshrajdhanapathyDD/reinvent2026-mcp)
server so any Kiro workspace can query the AWS re:Invent 2026 session catalog as
MCP tools — keyword + semantic search, venues, campus travel, and official links.

Author: **DD** · License: **MIT**

## What's inside

```
reinvent2026-power/
├── plugin.json                       # Power manifest (name, keywords, author)
├── mcp.json                          # Declares the stdio MCP server
├── skills/setup/SKILL.md             # Setup + usage + troubleshooting
└── dev.kiro/steering/reinvent2026.md # Agent guidance when the power is active
```

## Prerequisite

The power runs the `reinvent2026-mcp` command, so install the package once:

```bash
pip install reinvent2026-mcp
```

(If it's not on PATH, edit `mcp.json` to use `"command": "python", "args": ["-m", "reinvent2026_mcp.server"]`.)

## Install the power in Kiro

1. Open the **Powers** panel → **Add Custom Power** → **Import power from a folder**.
2. Select this `reinvent2026-power/` folder (the one containing `plugin.json`).
3. Kiro registers the power and its MCP server (auto-namespaced). Trigger it by
   mentioning re:Invent in chat, e.g. *"Search re:Invent 2026 for Bedrock chalk talks."*

The MCP server activates/deactivates with the power — nothing is written into
your global `mcp.json`.

## Tools

`catalog_status`, `search_sessions`, `semantic_search`, `get_session`,
`list_venues`, `estimate_travel`, `official_links`, `refresh_catalog`,
`load_catalog`.

See `skills/setup/SKILL.md` for full usage and troubleshooting.
