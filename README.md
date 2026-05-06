# Skillsstore for Claude Code

Your team's curated AI skills, in Claude Code. Marketplace + plugin
bundling the routing skill and the MCP connector for
[skillsstore.ai](https://skillsstore.ai).

## Install

```
/plugin marketplace add skillsstore/claude-code-plugin
/plugin install skillsstore@skillsstore
```

The first time Claude calls a Skillsstore tool, your browser will open to
authorise the connector against your workspace at
[skillsstore.ai](https://skillsstore.ai). OAuth 2.1 + PKCE — handled by
Claude Code natively.

## What you get

- **Routing skill** at `~/.claude/skills/skillsstore/` — tells Claude when
  to consult your workspace library: playbooks, brand-voice rules,
  code-review checklists, project standards, recurring task templates.
- **MCP connector** registered as `skillsstore` against
  `https://skillsstore.ai/api/mcp` (via the
  [`mcp-remote`](https://www.npmjs.com/package/mcp-remote) bridge).

Once installed and authorised, Claude proactively calls
`mcp__skillsstore__list_skills` / `search_skills` / `load_skill` whenever
your prompt overlaps with anything codified in your workspace.

## Repository layout

```
.claude-plugin/marketplace.json    ← marketplace catalog
plugins/skillsstore/
├── .claude-plugin/plugin.json     ← plugin manifest
├── .mcp.json                      ← MCP server config
└── skills/skillsstore/SKILL.md    ← routing skill
```

## Requirements

- Claude Code (latest, with plugin support)
- A Skillsstore workspace at [skillsstore.ai](https://skillsstore.ai)

## Other clients

This marketplace targets Claude Code. To use Skillsstore elsewhere:

- **Claude.ai / Claude Desktop** — Settings → Connectors → Add custom
  connector → `https://skillsstore.ai/api/mcp`
- **Cursor** — Settings → MCP → Add server, same URL
- **ChatGPT** (Plus/Team) — Settings → Connectors → MCP server, same URL
- **Zed** — `~/.config/zed/settings.json` → `context_servers`, same URL

## License

MIT — see [LICENSE](./LICENSE).
