# AgiFlow for Claude

Manage AgiFlow projects and tasks in Claude through the hosted AgiFlow MCP connector.

## Getting started

After installing the plugin, connect your AgiFlow account with OAuth. In Claude Code, use
`/mcp` to check the connection. Try asking Claude for a daily standup for your project.

## Features

This plugin connects to the AgiFlow MCP server (`https://agiflow.io/api/v1/mcp-app`) and exposes AgiFlow
tools across these categories:

- **Projects**: create, inspect, and update projects and their statuses
- **Tasks**: create, list, get, update, reorder, and batch-create tasks
- **Work units**: group tasks into deliverable features or epics and track progress
- **Members**: list workspace members and review task assignments
- **Comments**: document decisions and progress on tasks

### Bundled skills

This Directory bundle includes six project-management skills. Claude loads them when your request
matches their description.

| Skill | Phase | Use it to |
| --- | --- | --- |
| `getting-started` | orient | get coached on where to start and which workflow fits |
| `project-plan` | Planning | break requirements into vertical-slice tasks (Planning status) |
| `refine-task` | Planning | turn a vague task into an autonomous-ready spec |
| `backlog-grooming` | Planning → Todo | verify, prioritize, and promote tasks into work units |
| `triage` | diagnose | classify project issues by severity and recommend actions |
| `daily-standup` | report | a read-only pulse of done / in-progress / blocked / next |

Shared guidelines (status model, transitions, tags, work-unit sizing) live in
[`references/agiflow-agents.md`](references/agiflow-agents.md).

## Data handling and external services

The declared connector is `https://agiflow.io/api/v1/mcp-app`, authenticated with OAuth.
Agiflow can read and store names, email addresses, member profiles, tasks, comments, and artifacts
that you provide or authorize it to access. Workspace content is retained beyond 30 days unless
removed, subject to the [Privacy policy](https://agiflow.io/privacy-policy).

The bundled skills use only the declared AgiFlow connector. They do not run local programs,
execute scripts, or call other connectors.

**Optional analytics:** When configured by the AgiFlow deployment, the backend sends MCP usage
events to PostHog. These events can include user, organization, project, task, and session IDs,
client information, tool names, timing, success/error information, and submitted feedback.

See the [Terms of Service](https://agiflow.io/terms-and-conditions).

## License

MIT. See [LICENSE](LICENSE).
