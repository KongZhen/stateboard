# AGENTS.md

English is the canonical language for public project documentation. Every public-facing Markdown file that is meant for users should have a complete Chinese mirror beside it using the `.zh.md` suffix.

[中文](AGENTS.zh.md)

When entering this project, read first:

1. `README.md`
2. `docs/product-definition.md`
3. `docs/integration-matrix.md`
4. `docs/testing.md`
5. `skills/stateboard-codex/SKILL.md`

Project goal: turn AI work context into a project-status board. Do not reduce Stateboard to a generic todo bot.

Default principles:

- Establish the truth layer before judging tasks and priorities.
- Distinguish real task sync, calendar sync, and notification sync.
- Do not create automations until the user confirms the frequency and exact time.
- Do not split historical memory into many low-value tasks.
- Do not describe webhook notifications as a complete task system.
- Runtime language follows the user's request language unless the user explicitly asks for bilingual output.
