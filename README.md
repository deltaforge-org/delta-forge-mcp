# DeltaForge MCP Server

A Model Context Protocol (MCP) server that gives AI assistants (Claude, Cursor,
Codex, and any MCP client) first-class tools for DeltaForge: SQL analysis and
validation, command and documentation lookup, catalog and lineage browsing, and
pipeline inspection. The assistant can validate and explain SQL, trace
column-level lineage, search the docs, and read your catalog without you leaving
the chat.

Learn more at **[deltaforge.org](https://deltaforge.org)**.

DeltaForge is commercial software with a free Community license. See
[deltaforge.org/pricing](https://deltaforge.org/pricing).

## Run

```bash
npx deltaforge-mcp
```

On first run the native server binary for your platform is downloaded from this
repo's Releases and cached. Alternatively, install the native binary directly
from the [Releases](https://github.com/deltaforge-org/delta-forge-mcp/releases)
page (Linux/macOS tarball, Windows zip).

## Use with Claude

The server speaks MCP over stdio. Add it to Claude Desktop's config
(`claude_desktop_config.json`, reachable via Settings -> Developer -> Edit
Config), then restart Claude:

```json
{
  "mcpServers": {
    "deltaforge": {
      "command": "npx",
      "args": ["-y", "deltaforge-mcp"],
      "env": {
        "DELTAFORGE_CONTROL_PLANE_URL": "https://control.example.com"
      }
    }
  }
}
```

For Claude Code (CLI), register it once:

```bash
claude mcp add deltaforge -- npx -y deltaforge-mcp
```

Then ask Claude things like "validate this DeltaForge SQL", "show the lineage of
sales.public.orders", or "what schemas are in the catalog".

## Use with Codex

Add the server to your Codex config (e.g. `~/.codex/config.toml`):

```toml
[mcp_servers.deltaforge]
command = "npx"
args = ["-y", "deltaforge-mcp"]
env = { DELTAFORGE_CONTROL_PLANE_URL = "https://control.example.com" }
```

## Other clients

Cursor (`~/.cursor/mcp.json`) and any other MCP client use the same
`npx deltaforge-mcp` command. Ready-to-paste snippets for Claude, Codex, and
Cursor are in [`client-config/`](client-config/).

## Connect to your control plane

The SQL-analysis and documentation tools work offline. The catalog, lineage, and
pipeline tools need a DeltaForge control plane. Configure it from the assistant
via the `configure_control_plane` tool, or set:

- `DELTAFORGE_CONTROL_PLANE_URL`: control-plane URL
- a session token / personal access token (`df_pat_...`) when prompted

Auth uses a device-authorization flow with automatic token refresh.

## Tools

About 60 tools, grouped by area:

- **SQL analysis**: validate syntax, explain a query, classify statements,
  extract tables, column-level lineage, format SQL, generate external-table DDL.
- **Docs and commands**: list commands, get command syntax, search the docs, and
  format-specific references (Delta, Iceberg, graph, CSV, JSON, XML, Excel, Avro,
  ORC, Parquet, Protobuf, EDI, healthcare, geospatial, security).
- **Catalog**: list zones / schemas / tables / views / external tables, describe
  objects, column lists, table stats and properties, table history and schema
  evolution, upstream/downstream lineage.
- **Pipelines and workspace**: pipeline status, schedules, pipeline source,
  workspace files and overview.
- **Demos and CLI**: search demos, fetch a demo, generate CLI commands.

## What this repo is

A distribution and support home: release binaries, client-config examples, and
issue tracking. The MCP server is closed-source; its source is not published
here. Issues and questions:
[github.com/deltaforge-org/delta-forge-mcp/issues](https://github.com/deltaforge-org/delta-forge-mcp/issues).
