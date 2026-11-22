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
- **Workflows**: acquire and release locks and coordinate multi-agent runs
- **Members**: list and assign agent members to work
- **Comments**: document decisions and progress on tasks
- **Vault**: read and set scoped configuration entries

### Bundled skills

The plugin ships 10 workflow skills that mirror AgiFlow's scrum pipeline. Your AI client loads them on
demand when your request matches their description. You generally do not invoke them by name:

| Skill | Phase | Use it to |
| --- | --- | --- |
| `getting-started` | orient | get coached on where to start and which workflow fits |
| `project-plan` | Planning | break requirements into vertical-slice tasks (Planning status) |
| `refine-task` | Planning | turn a vague task into an autonomous-ready spec |
| `backlog-grooming` | Planning → Todo | verify, prioritize, and promote tasks into work units |
| `run-work` | Todo → Done | execute a whole work unit end-to-end in one session |
| `run-task` | Todo → Done | execute a single task through to Review |
| `review-work` | Review | verify acceptance criteria and file follow-ups |
| `triage` | diagnose | classify project issues by severity and recommend actions |
| `daily-standup` | report | a read-only pulse of done / in-progress / blocked / next |
| `orchestrate` | dispatch | route the highest-priority ready work to agents |

Shared guidelines (status model, transitions, tags, work-unit sizing) live in
[`references/agiflow-agents.md`](references/agiflow-agents.md).

## Data handling and external services

The declared connector is `https://agiflow.io/api/v1/mcp-app`, authenticated with OAuth.
Agiflow can read and store names, email addresses, member profiles, tasks, comments, and artifacts
that you provide or authorize it to access. Workspace content is retained beyond 30 days unless
removed, subject to the [Privacy policy](https://agiflow.io/privacy-policy).

Some workflows can send data beyond the declared Agiflow connector:

- **External MCP integrations:** When an allowed external tool is invoked through `task_exec` or
  `task_exec_code`, Agiflow forwards the tool arguments to the MCP server configured for your
  workspace and task. Destinations depend on the integrations you enable; there is no fixed
  third-party server list bundled with this plugin. Arguments can include project content and
  personal data supplied for the requested operation. The external provider's privacy policy applies.
- **Approved code scripts:** `task_exec_code` can call task-allowed MCP tools. An approved project
  script can also send HTTPS requests, including request bodies, to hosts permitted by its approved
  environment configuration. One-off code has no direct network access. Approving a script or tool
  can authorize reads and writes in an external service.
- **Coding-client tools:** Coding workflows instruct the AI client to use tools in your environment,
  including `vibe-lint`, local tests, Git, and pull-request tooling. Source code and project context
  can be passed to those tools or your configured Git hosting service. Their destinations depend on
  your client configuration.
- **Optional analytics:** When configured by the Agiflow deployment, the backend sends MCP usage
  events to PostHog. These events can include user, organization, project, task, and session IDs,
  client information, tool names, timing, success/error information, and submitted feedback.

Only send data to integrations and scripts you trust. Review their permissions and data handling
before enabling them. Also see the [Terms of Service](https://agiflow.io/terms-and-conditions).

## License

MIT. See [LICENSE](LICENSE).
