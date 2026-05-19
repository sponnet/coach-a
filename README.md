# AI Team Template — Larry + Nolan + Pax

A minimal Claude Code starter for a Larry-orchestrated AI team. Clone this repo, open it in Claude Code, and you have a working multi-agent setup out of the box.

## What's included

| File / Folder | Purpose |
|---|---|
| `CLAUDE.md` | Larry — the orchestrator persona. Claude Code reads this on every session. |
| `DATABASE.md` | Schema reference for the shared SQLite database. |
| `team.db` | Empty SQLite database (WAL mode). Shared across all agents. |
| `.claude/settings.local.json` | Permissions + auto-memory disabled. |
| `.claude/agents/nolan.md` | Nolan subagent — HR Manager, creates new team members. |
| `.claude/agents/pax.md` | Pax subagent — Senior Researcher, produces Skills Profiles. |
| `team/agent-index.md` | Routing table. Larry reads this on every request. |
| `team/Nolan - HR Manager/AGENTS.md` | Nolan's full persona contract. |
| `team/Pax - Senior Researcher/AGENTS.md` | Pax's full persona contract. |
| `team-inbox/` | Drop task files here for multi-step workflows between agents. |
| `projects/` | One subfolder per project. Each must have a `public/` subfolder. |

## Prerequisites

- [Claude Code](https://claude.ai/code) installed (`npm install -g @anthropic-ai/claude-code` or via the desktop app)
- An Anthropic API key

## Getting started

```bash
# 1. Clone the repo
git clone <your-repo-url>
cd <repo-name>

# 2. Open in Claude Code
claude .
```

Claude Code will load `CLAUDE.md` automatically and Larry will be active immediately.

## How the team works

**Larry** (the top-level session) never does domain work himself. He routes every request to the right specialist.

Only two specialists exist at the start:

- **Pax** — researches what expertise is needed for a new domain
- **Nolan** — turns Pax's research into a fully designed AI team member

### Hiring your first specialist

Just describe what you need. Larry will:

1. Ask Pax to research the required skills
2. Ask Nolan to design and create the new team member
3. Delegate your original task to the new hire

Example prompts:
> "I need someone who can help me with my garden."
> "Hire a frontend developer who can build dashboards."
> "I need a dietitian to help me plan weekly menus."

### Starting a new project

Create a folder under `projects/` with a `public/` subfolder inside:

```
projects/
  my-project/
    public/        ← publishable output goes here
    notes/         ← private working files
```

## Folder conventions

- **`projects/<name>/public/`** — clean, shareable output only (no drafts, no private notes)
- **`team-inbox/`** — task handoff files between agents in multi-step workflows
- **`team.db`** — shared SQLite database; document every table in `DATABASE.md`

## Customising the setup

- **Add MCP tools** (Spotify, Gmail, Calendar, etc.) via Claude Code settings and reference them in the relevant agent's `tools:` frontmatter.
- **Add permissions** to `.claude/settings.local.json` as your agents need them (e.g. `Bash(git commit:*)` for agents that commit).
- **Extend `DATABASE.md`** whenever an agent creates a new table.

## Auto-memory

Auto-memory is disabled in `.claude/settings.local.json`. To enable it, add:

```json
"autoMemoryDirectory": "~/memory/<your-project-name>"
```
