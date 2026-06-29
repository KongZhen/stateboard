# Stateboard Automation Prompt

[中文](stateboard-automation-prompt.zh.md)

This is an advanced template for agents after the user has confirmed frequency and exact run time through `stateboard-sync-prompt.md`. Ordinary users should not need to fill this in directly.

```text
Run Stateboard sync on the confirmed frequency and schedule.

Schedule:
[Daily/weekly + exact time, for example Monday 09:00 every week]

Source scope:
[Fixed readable scope, for example a specific repository, project notes, existing task exports, or selected context files]

Target:
[Destination system and target list/project/database]

Existing mapping:
[Existing destination task ID mapping; if unavailable, search stable titles first, then create]

Granularity:
[Compact overview / balanced project tasks / detailed next-action plan]

Rules:
- Read the truth layer before judging project state.
- Update existing tasks first. Do not duplicate them.
- Create durable project tasks only for real active projects.
- Put dormant or low-evidence projects into a parking lot.
- Do not write secrets, tokens, webhook URLs, webhook secrets, license keys, credentials, or private destination identifiers.
- If the target connector is unavailable, output a Markdown fallback and mark the run as blocked. Do not call private APIs.
- Respond and write destination content in the language of the user's request unless the user explicitly asks for bilingual output.
- Output a short run report covering created, updated, skipped, verified, and blocked items.

If schedule, source scope, target, or existing mapping is missing, ask first. Do not create automation.
```
