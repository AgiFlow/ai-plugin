---
name: agiflow-getting-started
description: "Get oriented in AgiFlow and drive its core workflows through the plugin's MCP tools. Use this when the user wants to explore AgiFlow products, flows, journeys, tasks, or work units, or asks how to start using the AgiFlow plugin. Trigger on mentions of `AgiFlow`, `agiflow.io`, or 'AgiFlow plugin'."
tags:
  - agiflow
  - mcp
  - getting-started
  - workflows
---

# AgiFlow Getting Started

Orient the user inside [AgiFlow](https://agiflow.io) and help them act on its core entities —
products, flows, journeys, tasks, and work units — using the MCP server wired into this plugin.

## Prerequisites

- The AgiFlow MCP server is configured (`.mcp.json` → server `agiflow`, endpoint
  `https://agiflow.io/api/v1/mcp`, header `x-agiflow-mcp-consumer: plugin`).
- The host (Codex / Claude Code / Cursor / Gemini CLI) has loaded this plugin and the MCP server is
  reachable. If tool calls fail, confirm connectivity and auth before continuing.

## When To Use

- The user is new to AgiFlow and asks "what can I do here?"
- The user wants to list or inspect AgiFlow products, flows, journeys, or the product map.
- The user wants to find, create, or update tasks and work units.

## Workflow

1. **Establish context.** Discover what the AgiFlow MCP server exposes before acting — list the
   available capabilities/tools, then list products so you know which one the user means.
2. **Pick the entity.** Map the user's intent to the right surface:
   - Products & structure → product list / product map / domains
   - Flows & journeys → list/get flow, list/get journey
   - Execution → list/create/update tasks and work units
3. **Read before write.** Always fetch the current state (get the task/work unit/flow) before
   proposing a create or update, so you don't duplicate or overwrite existing records.
4. **Confirm mutations.** Summarize what you're about to create or change and confirm with the user
   before any write/update tool call.
5. **Report outcomes faithfully.** Quote the IDs/links the MCP server returns; if a call fails,
   surface the error rather than guessing success.

## Notes

- Do not assume endpoints, IDs, or ports — resolve them from the MCP tool responses.
- Keep new reusable AgiFlow instructions in `skills/`; put autonomous helpers in `agents/`.
