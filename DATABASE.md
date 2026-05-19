# Database Reference

The team's shared SQLite database lives at `./team.db` (repo root).

All agents that read or write data must consult this file first.

## Conventions

- **WAL mode** — enable on first connection: `PRAGMA journal_mode=WAL;`
- **Parametrized queries only** — no string interpolation in SQL.
- **Append-only tables** where noted — never UPDATE or DELETE without a documented reason.
- **Never commit** `team.db-wal` or `team.db-shm` files.

## Shared tables

Add shared tables here as the team grows. Each entry should include:
- Table name
- Purpose (one line)
- Column definitions
- Which agent owns / writes it

## Project → Tables → Agent quick map

| Project | Owner agent | Primary tables |
|---|---|---|
| _(add rows as projects are created)_ | | |

---

_This file is maintained by the team. Update it whenever a new table is created._
