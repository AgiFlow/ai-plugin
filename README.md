# Agiflow AI Plugin

This repository packages the Agiflow plugin for Codex, Claude Code, Cursor, and Gemini CLI.

## Layout

- `.codex-plugin/plugin.json` for Codex
- `.claude-plugin/plugin.json` for Claude Code
- `.cursor-plugin/plugin.json` for Cursor
- `references/plugin-types.md` for client compatibility notes
- `.mcp.json` and `mcp.json` for MCP client wiring
- `gemini-extension.json` and `GEMINI.md` for Gemini CLI

## Development

Clone the repo, then load it from your tool of choice as a local plugin bundle.
Keep new skills in `skills/` and new reusable agents in `agents/`.

The repo root is `agiflow-ai-plugin`.
