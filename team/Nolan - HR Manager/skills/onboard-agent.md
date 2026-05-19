# Skill: Onboard a New Agent (Full File Creation)

## Trigger

Use this skill after completing `design-persona` to create all the files a new agent needs.

## Steps

### 1. Create the agent folder and rich contract
```
team/<Name> - <Role>/
  AGENTS.md              ← rich contract (persona, capabilities, boundaries)
  prompts/
    role.md              ← core role instructions (identity, communication style, ownership)
  skills/
    <primary-skill>.md   ← at least one skill file for their main task
```

### 2. Write `AGENTS.md`
Use the persona designed in the `design-persona` skill. Include:
- Identity block (name, role, reports-to)
- Persona paragraph
- Communication style
- Primary responsibilities (numbered)
- Output convention (always: final deliverables → `projects/<project>/public/`)

### 3. Write `prompts/role.md`
Extract the stable identity content from AGENTS.md into a standalone prompt file:
- Who they are (persona)
- Communication style
- What they own

### 4. Write at least one `skills/<skill>.md`
Cover the agent's primary task as a step-by-step skill. See existing skill files for format.

### 5. Create the subagent file
Write `.claude/agents/<name>.md` with:
```markdown
---
name: <name>
description: <one-sentence routing description for Larry>
tools: <comma-separated list>
---

You are <Name>, <Role> of the team.

On every invocation, in order:
1. Read `team/<Name> - <Role>/AGENTS.md` — your full operating contract.
2. Read `team/<Name> - <Role>/prompts/role.md` — your core role instructions.
3. Read `CLAUDE.md` at the repo root for Larry's orchestration rules.

<Any additional cold-start instructions specific to this agent.>

Output convention: final deliverables go in `projects/<project>/public/`. Working notes stay outside `public/`.
```

### 6. Update `team/agent-index.md`
Add a row to the routing table with: Specialist, Role, Folder, Subagent, Route-to-them-when.

### 7. Report to Larry
Confirm: name, role, files created, and what task they're ready to handle.
