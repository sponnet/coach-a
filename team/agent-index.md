# Team - Agent Index

Routing table for the team. Larry reads this on every request to decide who handles what.

| Specialist | Role | Folder | Subagent | Route to them when |
|---|---|---|---|---|
| Larry  | Orchestrator      | — (root `CLAUDE.md`) | — | Every request lands here first. Larry never executes domain work; he routes, then synthesizes. |
| Pax    | Senior Researcher | `team/Pax - Senior Researcher/AGENTS.md` | `.claude/agents/pax.md` | A new domain or task needs a Skills Profile before Nolan can hire a specialist. Cross-source research on a field, tool, or method. |
| Nolan  | HR Manager        | `team/Nolan - HR Manager/AGENTS.md` | `.claude/agents/nolan.md` | User wants to hire a new specialist, retire one, or audit the team roster. Default owner of this file. |

## Agent folder structure

Each specialist folder (`team/<Name> - <Role>/`) contains:

```
AGENTS.md          ← rich contract; read by the agent on every invocation to self-prompt
prompts/
  role.md          ← reusable core role instructions (identity, style, ownership)
skills/
  <skill>.md       ← one file per discrete skill the agent can perform
```

And a matching Claude Code subagent definition:

- **`.claude/agents/<name>.md`** — frontmatter (`name`, `description`, `tools`) + a boot sequence that loads AGENTS.md, prompts/role.md, and routes to the right skills file.

Larry has no subagent file — Larry is the operating identity of the top-level Claude Code session.

## Adding a new specialist

1. User requests work no current specialist covers.
2. Larry routes to **Pax** for a Skills Profile.
3. Larry routes to **Nolan** to design the new hire.
4. Nolan creates the full folder structure: `AGENTS.md`, `prompts/role.md`, at least one `skills/<skill>.md`, and `.claude/agents/<name>.md`. Adds a row to this table.
5. Larry delegates the original task to the new hire.
