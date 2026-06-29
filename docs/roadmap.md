# Roadmap

[中文](roadmap.zh.md)

## Phase 1: Reproducible Entry Points

- Maintain and test both entry points: copyable prompt and `stateboard-codex` skill.
- Provide `prompts/stateboard-sync-prompt.md` as a one-fill quickstart for ordinary users; keep the automation prompt as an advanced implementation template.
- Keep `stateboard-codex` installable from `skills/stateboard-codex/`.
- Provide Markdown dry-run testing before any external write.
- Document optional live-sync testing in `docs/testing.md`.
- Keep automation gated by user-confirmed frequency and exact run time.

## Phase 2: Core Schema

- Extract `ProjectState`.
- Extract `TaskSink`, `CalendarSink`, and `NotificationSink`.
- Define idempotent update rules and ID mapping.
- Define task granularity rules.

## Phase 3: Adapters

- Dida / TickTick adapter.
- Google Calendar review block.
- Notion dashboard.
- Feishu/Lark tasks + reminders + bot card prototype.

## Phase 4: Open-Source Distribution

- Use MIT license.
- Keep English as canonical public documentation with complete Chinese mirrors.
- Provide a bilingual GitHub Pages introduction.
- Keep public examples generic and free of private project history.
- Maintain the project as alpha until the core schema and first adapters are stable.
