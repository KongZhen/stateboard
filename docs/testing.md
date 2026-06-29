# Testing

[中文](testing.zh.md)

Use this checklist before publishing changes to prompts, skills, or integration docs.

## Prompt

1. Copy `prompts/stateboard-sync-prompt.md` into an AI assistant.
2. Fill the four user-facing fields:
   - what to organize
   - destination
   - target location
   - automatic refresh
3. Run a Markdown-only dry-run first.
4. Confirm the output contains:
   - one project-status task per real active project
   - 3-5 useful next actions per task
   - current progress, blockers, priority, and evidence
   - a clear run report

## Skill

1. Install the skill:

   ```bash
   cp -R skills/stateboard-codex ~/.codex/skills/stateboard-codex
   ```

2. Start a new Codex thread and run:

   ```text
   $stateboard-codex

   What to organize: the current project
   Destination: Markdown only
   Target location: reply directly here
   Automatic refresh: not needed
   ```

3. Confirm the skill follows the same behavior as the prompt.

## Optional Live Sync

Only run a live sync when the user has chosen a destination and confirmed write permission.

Use a dedicated test list or page. Do not use private production lists for first tests.

Check that:

- existing tasks are searched before new tasks are created
- a second run updates the same task instead of creating a duplicate
- no token, webhook secret, license key, credential, or private destination identifier appears in task bodies or public files
- no recurring automation is created without confirmed frequency and exact time

## Automation Gate

Automation can be created only after the user provides:

- source scope
- target system and target location
- frequency
- exact run time
- language preference when sources are mixed-language

If any of these are missing, ask before creating or updating automation.
