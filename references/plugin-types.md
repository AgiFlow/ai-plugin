# AI Plugin Client Types

Use this reference when updating this plugin repo for a supported coding agent client.

## Codex

- Primary manifest: `.codex-plugin/plugin.json`
- Common companion paths: `skills/`, `.mcp.json`, `.app.json`, `assets/`, `agents/`, `commands/`
- Use `mcpServers` only when `.mcp.json` exists.
- Keep `skills` pointing at `./skills/`.

## Claude Code

- Primary manifest: `.claude-plugin/plugin.json`
- Components live at plugin root, not under `.claude-plugin/`.
- Common component paths: `skills/`, `commands/`, `agents/`, `hooks/`, `.mcp.json`, `.lsp.json`, `monitors/`, `bin/`, `settings.json`
- Prefer `skills/` for new reusable instructions.

## Gemini CLI

- Primary extension manifest: `gemini-extension.json`
- Common companion file: `GEMINI.md`
- Supports `mcpServers` in the extension manifest and variable substitution for settings.

## Cursor

- Cursor's stable integration surface for this scaffold is MCP configuration.
- `.cursor-plugin/plugin.json` is local compatibility metadata, not an official install manifest unless Cursor publishes that contract.

## Antigravity (Google)

- A plugin is a directory with a root `plugin.json` marker file. `name` is optional and defaults to the directory name.
- Component paths: `skills/<name>/SKILL.md` (same SKILL.md format as Claude Code), `rules/<name>.md`, `mcp_config.json`, `hooks.json`.
- MCP wiring lives in root `mcp_config.json` using `{ "mcpServers": { "<name>": { "serverUrl": "...", "headers": {...} } } }`. Antigravity uses `serverUrl` (not `type`/`url`) for remote Streamable HTTP servers; `command`/`args`/`env`/`cwd` for stdio.
- Installed from `.agents/plugins/`, `_agents/plugins/` (workspace), or `~/.gemini/config/plugins/` (global).
- Source reference: https://antigravity.google/docs/plugins and https://antigravity.google/docs/mcp

## MCP

- Primary config: `.mcp.json` (Codex/Claude, `type: http` + `url`)
- Broad client compatibility config: `mcp.json`
- Antigravity config: `mcp_config.json` (`serverUrl` + `headers`)
- Default consumer header: `x-<product>-mcp-consumer: plugin`
- Do not guess service URLs or ports; add MCP wiring only when the endpoint is known.
