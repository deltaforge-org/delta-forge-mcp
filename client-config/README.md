# MCP client configuration

Ready-to-paste configuration for connecting an MCP client to the DeltaForge MCP
server. Each uses `npx deltaforge-mcp`, which downloads and caches the native
server binary on first run.

| Client | File | Where it goes |
| --- | --- | --- |
| Claude Desktop | [`claude_desktop_config.json`](claude_desktop_config.json) | `claude_desktop_config.json` (Settings -> Developer -> Edit Config) |
| Cursor | [`cursor_mcp.json`](cursor_mcp.json) | `~/.cursor/mcp.json` (or the project `.cursor/mcp.json`) |
| Codex | [`codex_config.toml`](codex_config.toml) | your Codex config, e.g. `~/.codex/config.toml` |

Set `DELTAFORGE_CONTROL_PLANE_URL` to your control plane. The SQL-analysis and
documentation tools work without it; the catalog, lineage, and pipeline tools
need it. The first catalog call triggers a device-authorization sign-in.

If you installed the native binary instead of using `npx`, replace
`"command": "npx", "args": ["-y", "deltaforge-mcp"]` with
`"command": "/path/to/deltaforge-mcp"`.
