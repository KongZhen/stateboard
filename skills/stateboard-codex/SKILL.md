---
name: stateboard-codex
description: Use when a user wants AI project context from Codex, ChatGPT, Claude, DeepSeek, WorkBuddy, local repos, project notes, chats, or selected context files organized into a Stateboard-style project dashboard and synced into todo, calendar, or collaboration tools such as TickTick/Dida, Feishu/Lark, DingTalk, WeCom, Microsoft To Do, Apple Reminders, or Google Calendar.
metadata:
  short-description: Sync AI project state into Stateboard
---

# Stateboard Codex

[中文](SKILL.zh.md)

Turn scattered AI project context into a maintained Stateboard: a living project-status dashboard that can sync into the user's preferred todo, calendar, documentation, or collaboration system.

This skill is for project-state maintenance, not generic todo capture. It should produce a small set of durable project tasks, each with current status, priority, next actions, blockers, and evidence.

## When To Use

Use this skill when the user asks to:

- organize projects currently being advanced in Codex / ChatGPT
- organize project conversations from Claude / DeepSeek / WorkBuddy / other AI tools
- sync to 滴答清单 / TickTick / Dida / Microsoft To Do / Apple Reminders / Calendar / other todo apps
- sync to 飞书 / Lark, 钉钉 / DingTalk, 企业微信 / WeCom, or similar collaboration platforms
- turn project status into tasks automatically
- update project lists daily or weekly
- turn ChatGPT/Codex context into a project management board

Do not use this skill for one-off reminders such as "tomorrow remind me to call X" unless the user also asks to organize project context.

## Core Idea

The output is not "AI writes todos".

The output is:

```text
project evidence -> project judgment -> durable task dashboard -> optional scheduled refresh
```

## Required Intake

Before creating tasks or recurring automation, ask the user for missing required fields in plain language. Do not silently default to 03:00 or any fixed time.

User-facing intake:

1. What to organize: which conversations, projects, folders, notes, tasks, or pasted material should be included?
2. Destination: which app or output format should receive the project board?
3. Target location: which list, project, page, database, calendar, or Markdown output should be used or created?
4. Automatic refresh: not needed, or a specific daily/weekly frequency and exact time.
5. Detail level only when needed: default to balanced project tasks unless the user asks for a compact overview or detailed next-action plan.

If the user already supplied a value, do not ask again. If several values are missing, ask them together in one concise message. Do not expose internal terms such as `source scope`, `ProjectState`, or `task id mapping` unless the user is configuring automation or debugging idempotency.

Use this wording when time is missing, translated to the user's language when needed:

```text
What time should the project-state automation run? Good choices are times when you are unlikely to be actively editing, such as 07:30, 09:00, 18:30, or 22:30. You can also choose a weekly time instead.
```

## Runtime Language

Respond and write destination content in the language of the user's request unless the user explicitly asks for bilingual output.

- English request -> English project tasks, task bodies, and run report.
- Chinese request -> Chinese project tasks, task bodies, and run report.
- Mixed request -> follow the explicit language preference; if unclear and an external write is about to happen, ask once before writing.

## Source Access Boundary

Only use content that is currently readable, searchable, connected through an available tool, or provided by the user. Do not imply access to another AI product's private history unless the user pasted, uploaded, connected, or authorized that data.

If requested sources are unavailable, ask for the missing material or continue with a clearly labeled partial view.

## Connector Discovery

1. Identify the target app.
2. Search available tools before assuming write access:
   - TickTick/Dida: search `滴答清单 dida365 ticktick task project create update search`
   - Google Calendar: search `google calendar event create update`
   - Feishu/Lark, DingTalk, WeCom: read `references/integration-support.md` and distinguish real task sync, calendar sync, and notification-only sync.
   - Microsoft / Outlook / To Do: search available connectors first; if absent, use export/fallback.
   - Apple Reminders / Calendar: use available local automation only if explicitly enabled; otherwise provide importable text/calendar fallback.
3. If no connector exists, do not use private APIs. Produce a structured fallback:
   - Markdown task dashboard
   - CSV-like import table
   - calendar/reminder creation instructions
   - app-specific URL scheme only when official or app-store documentation exposes it
   - a clear note that no external write happened

## Default Workflow

1. **Establish the truth layer.**
   - Read the smallest useful continuity set: project notes, current-state docs, repo status, existing tasks, and recent evidence.
   - Prefer current files and known automation state over stale summaries.
   - Separate confirmed facts, assumptions, blockers, and open questions.

2. **Create a project inventory.**
   - One row per real project/workstream.
   - Capture: name, positioning, status, priority, next action, blocker, evidence date.
   - Avoid turning every historical note into a task.

3. **Choose task granularity.**
   - Default: balanced project tasks.
   - Use `references/task-granularity-rubric.md`.
   - Keep most projects as one parent task plus 3-5 checklist items.
   - Use a single parking-lot task for low-signal dormant projects.

4. **Map to the target app.**
   - Use `references/todo-app-capability-matrix.md`.
   - Preserve stable task titles and IDs for idempotent updates.
   - Use tags such as `codex-sync`, project slug, and priority.
   - Do not mark project tasks complete during a sync unless the user explicitly says the project is done.

5. **Set up automation only when requested.**
   - Use the user-confirmed schedule.
   - Prefer updating an existing automation over creating a duplicate.
   - Automation prompt must include:
     - target app/list identifiers
     - existing task ID mapping
     - source directories, project notes, or selected context files
     - update-not-duplicate rule
     - verification step
     - runtime language rule
   - If the current environment cannot create automation, provide copy-ready setup instructions and do not claim automation was created.

6. **Verify.**
   - After writing, search/fetch the destination for key tasks.
   - If search indexing is delayed, rely on write-tool return values and say search may lag.
   - If automation was created or updated, verify the automation configuration is active and uses the confirmed schedule.

## Priority Rubric

Use this default priority model unless the user supplies a different one:

- `P0`: active this week, high urgency, current user attention, or release/blocker pressure.
- `P1`: important ongoing project requiring decisions, verification, or coordination.
- `P2`: meaningful but lower-frequency workstream with a stable baseline.
- `P3`: parking lot, context retained, no immediate action unless reactivated.

Map to app priorities conservatively:

- P0/P1 -> high priority if the app has only a few levels.
- P2 -> normal priority.
- P3 -> low priority or no due date.

## Task Shape

Default title:

```text
P1 | Project Name: one-line positioning
```

Default body:

```text
Positioning:
Current progress:
Priority:
Risks / boundaries:
Recommended next steps:
Evidence:
```

Default checklist:

```text
- Confirm current truth layer
- Resolve next decision
- Run verification / review
- Update project note or dashboard
```

Translate labels and task body language to the user's request language.

## Guardrails

- Do not claim market ranking unless a current ranking source was actually checked.
- Do not duplicate tasks when an existing list/task can be updated.
- Do not over-fragment project history into dozens of tasks.
- Do not write secrets, tokens, private keys, license keys, personal credentials, or private destination identifiers into task descriptions.
- Do not create recurring automations without confirming time and frequency.
- Do not pretend to access unavailable chats, tools, lists, calendars, or automation systems.
- Do not change project code while performing a project-state sync.
- Do not treat archived or dormant projects as active just because memory contains them.

## References

- `references/todo-app-capability-matrix.md`
- `references/integration-support.md`
- `references/task-granularity-rubric.md`
- `references/top-skill-benchmark.md`
- `templates/intake-questions.md`
- `templates/sync-report-template.md`
- `templates/task-id-mapping-template.md`
- `examples/stateboard-demo-dry-run.md`

## Output Summary

When done, report in the user's request language:

- destination created/updated
- number of tasks created/updated
- verification result
- automation name, schedule, and status, or "not created / awaiting confirmed time"
- unresolved connector or permission limits
