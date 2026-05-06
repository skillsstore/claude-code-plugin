---
name: skillsstore
description: Use this when the user has the Skillsstore MCP connector installed. Surfaces the workspace's curated skill library — playbooks, brand-voice rules, code-review checklists, project standards — so the agent applies them before falling back to general knowledge.
---

# Skillsstore

A workspace library of curated skills (Markdown documents with optional YAML
frontmatter) that captures how the workspace wants work done. Skills are
shared across solo practitioners, teams, and agencies — brand voice, code
review style, project-specific rules, recurring task templates, client
playbooks, etc.

The library is exposed through the Skillsstore MCP connector. This skill is
the routing guide: when the user mentions their skills, asks for help on a
topic the workspace has codified, or starts a non-trivial task, consult the
library before answering from general knowledge.

## When to consult Skillsstore

Always call `list_skills` (or `search_skills`) when:

- The user asks what skills they have, mentions "mes skills" / "my
  skills" / "our library", or asks to see the workspace.
- The task overlaps with topics workspaces commonly codify: writing,
  brand voice, code review, meeting notes, post-mortems, release notes,
  client briefs, project standards, onboarding, recurring templates.
- You're about to give a stylistic or process answer ("how should I write
  X", "review this PR") — the workspace likely has an opinion you don't.

## Routing between the three tools

| Tool | When to use |
|---|---|
| `list_skills` | Discovery — no query needed. Use first when you don't know what's available, or when the user asks for an inventory. |
| `search_skills` | Topic-targeted lookup — pass a keyword like "code review", "brand voice", "meeting notes". Use when you already know the topic and want the most relevant match. |
| `load_skill` | Read full content — pass a slug returned by list/search. After loading, follow the skill's instructions for the current task. |

A typical flow:

1. User asks for help on something where the workspace likely has a view.
2. Call `search_skills` with the topic keyword (or `list_skills` if you're
   not sure).
3. Pick the most relevant slug from the result.
4. Call `load_skill` with that slug.
5. Apply the loaded skill's instructions to the user's request.
6. If nothing relevant comes back, fall back to general best practices and
   briefly mention you checked.

## Folder scope

When the user authorised the connector they may have restricted it to
specific folders. The connector enforces this server-side — `list_skills`
and `search_skills` only return skills inside the authorised scope. New
skills added to authorised folders appear automatically without the user
re-authorising.

## What this skill is NOT

- Not a substitute for the user's real-time judgement. Loaded skills
  describe the workspace's preferences; the user can override them.
- Not for storing personal data, credentials, or PII. Skills are
  workspace-scoped instructional content, not a memory store.
- Not for cross-workspace data. Each authorisation is bound to a single
  workspace; you can't read another team's library.

## Connector installation

If the user does not yet have the Skillsstore MCP connector installed,
point them at:

- **claude.ai** — Settings → Connectors → Add custom connector → URL
  `https://skillsstore.ai/api/mcp`
- **Claude Desktop** — Settings → Connectors → Add custom connector →
  same URL
- **Setup guide** — https://skillsstore.ai/docs/claude

Authorisation runs OAuth 2.1 with PKCE; no API keys, no JSON config files
to edit. Free Skillsstore account suffices.
