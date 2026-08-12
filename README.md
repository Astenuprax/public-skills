# public-skills

Publicly shared, self-contained agent skills. Each subfolder is one skill —
drop-in for Claude Code, Claude.ai, or any assistant that reads a `SKILL.md`.

| Skill | What it does |
|---|---|
| [`claim-review`](claim-review/) | Strengthen a claim to its strongest form, then check whether its evidence actually supports it. |
| [`skill-architect`](skill-architect/) | Author, audit, and update agent skills, putting each through a three-part Quality Gate before you trust it. |

Each skill folder is self-contained (`SKILL.md` + `README.md` + `LICENSE`, plus any
per-platform builds under `exports/`) and carries no dependency on private
governance. Licensed MIT unless a skill states otherwise.
