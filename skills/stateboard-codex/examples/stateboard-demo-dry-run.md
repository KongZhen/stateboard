# Stateboard Demo Dry-Run Example

[中文](stateboard-demo-dry-run.zh.md)

This dry-run example verifies that `stateboard-codex` can produce an inspectable project-status task even when no external connector is available or writes are not allowed.

## Input

```text
What to organize: the current Stateboard repository
Destination: Markdown only
Target location: reply directly here
Automatic refresh: not needed
```

## Expected Output

```text
Title:
P1 | Stateboard: AI work-context project board

Positioning:
Turn Codex / ChatGPT / agent work context into a living project-status board and sync it to todo, calendar, and collaboration tools.

Current progress:
Product definition, prompt entry, skill entry, integration model, and public testing checklist are documented. V1 keeps both the prompt quickstart and Codex skill.

Priority:
P1. The current focus is verifying that both prompt and skill entry points can generate project-status tasks and update the same destination task.

Risks / boundaries:
- Do not reduce Stateboard to a generic todo assistant.
- Do not describe webhook notifications as a complete task system.
- Do not create automation without confirmed frequency and exact time.
- Do not split historical context into low-value tasks.

Recommended next steps:
- Keep prompt and skill testing guidance up to date.
- Use the task ID mapping template with placeholders for idempotent update rules.
- Test recurring sync only after automation timing is confirmed.

Evidence:
- docs/product-definition.md
- docs/prompt-template.md
- docs/testing.md
- skills/stateboard-codex/SKILL.md
```

## Acceptance

- Output contains one project-status task.
- Evidence sources are explicit.
- No external write occurs.
- No token, webhook secret, license key, private task ID, or private destination ID appears.
