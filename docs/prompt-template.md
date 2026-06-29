# Stateboard Prompt Template

[中文](prompt-template.zh.md)

This document is the prompt entry index. It avoids maintaining duplicate prompt templates in multiple places.

Canonical copyable template:

- `prompts/stateboard-sync-prompt.md`: ordinary user entry point; the user fills it once, covering both manual sync and automatic refresh intent.

Chinese mirror:

- `prompts/stateboard-sync-prompt.zh.md`

Advanced template:

- `prompts/stateboard-automation-prompt.md`: for agents after the user has already confirmed automation frequency and exact time. Ordinary users do not need to fill it directly.
- `prompts/stateboard-automation-prompt.zh.md`: Chinese mirror.

## Usage

- Zero-install quick validation: copy `prompts/stateboard-sync-prompt.md`.
- Long-term reuse: install and use `skills/stateboard-codex/`.
- Recurring automation: still start with `prompts/stateboard-sync-prompt.md` and write the confirmed frequency and exact time in "Automatic refresh".

## Minimum Test Input

```text
What I want to organize:
The current Stateboard project, or the project at <your-project-path>

Sync to:
Dida/TickTick

Target location:
Create a new list called Project Status Test

Automatic refresh:
Not needed
```

## Required Constraints

- Establish the truth layer before judging project state.
- Only organize content the current model can read or the user has provided.
- Search before writing; update the same task when possible.
- Do not split historical memory into many low-value tasks.
- Do not create automation without confirmed frequency and exact time; if the current environment cannot create automation, do not pretend it was created.
- Do not write tokens, webhook secrets, license keys, credentials, or private destination identifiers.
- Respond and write destination content in the user's request language unless bilingual output is explicitly requested.
