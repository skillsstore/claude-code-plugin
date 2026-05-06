# Skillsstore for Claude Code

Your team's curated AI skills, in Claude Code. One install bundles the
routing skill and the MCP connector — no separate `claude mcp add`,
no manual auth flow.

## Install

```
/plugin install https://github.com/skillsstore/claude-code-plugin
```

The first time Claude calls a Skillsstore tool, your browser will open to
authorise the connector against your workspace at
[skillsstore.ai](https://skillsstore.ai). OAuth 2.1 + PKCE — handled by
Claude Code natively.

## What this plugin does

- Registers `https://skillsstore.ai/api/mcp` as an MCP server in Claude
  Code (via [`mcp-remote`](https://www.npmjs.com/package/mcp-remote) bridge).
- Installs a routing skill at `~/.claude/skills/skillsstore/` that tells
  Claude when to consult your workspace library — playbooks, brand-voice
  rules, code-review checklists, project standards, recurring task
  templates.

Once installed and authorised, Claude proactively calls
`mcp__skillsstore__list_skills` / `search_skills` / `load_skill` whenever
your prompt overlaps with anything codified in your workspace.

## Requirements

- Claude Code (latest version with plugin support)
- A Skillsstore workspace at [skillsstore.ai](https://skillsstore.ai)

## Configuration

Folder scoping, OAuth lifecycle, and per-skill permissions are managed
inside the Skillsstore dashboard — no local config needed.

## Other clients

This plugin is Claude Code-specific. To use Skillsstore with other MCP
clients:

- **Claude.ai / Claude Desktop** — Settings → Connectors → Add custom
  connector → `https://skillsstore.ai/api/mcp`
- **Cursor** — Settings → MCP → Add server, same URL
- **ChatGPT** (Plus/Team) — Settings → Connectors → MCP server, same URL
- **Zed** — `~/.config/zed/settings.json` → context_servers, same URL

## License

MIT — see [LICENSE](./LICENSE).
