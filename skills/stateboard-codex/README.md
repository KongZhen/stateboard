# Stateboard Codex Skill

[中文](README.zh.md)

This is Stateboard's first Codex skill. It turns project context from Codex, ChatGPT, Claude, DeepSeek, WorkBuddy, local repositories, chats, and project notes into a maintained project-status board, then syncs it to todo, calendar, or collaboration tools.

It only uses content that the current environment can read, search, or that the user has provided. If some conversations or project materials are unavailable, it must say so instead of pretending they were read.

Supported destination shapes include:

- 滴答清单 / TickTick / Dida MCP
- Microsoft To Do / Outlook / Windows Focus Sessions
- Apple Reminders / Apple Calendar
- 飞书 / Lark tasks, calendar, and bots
- 钉钉 / DingTalk todos, schedules, and bots
- 企业微信 / WeCom calendar, app messages, and group bots
- Markdown, CSV-like, or URL-scheme fallback for other todo apps

## Install

Copy the whole folder into the Codex skills directory:

```bash
cp -R skills/stateboard-codex ~/.codex/skills/stateboard-codex
```

Then use it in Codex:

```text
$stateboard-codex
```

## Quickstart

Minimum dry-run:

```text
$stateboard-codex

What to organize: the current Stateboard repository
Destination: Markdown only
Target location: reply directly here
Automatic refresh: not needed
```

Minimum live sync:

```text
$stateboard-codex

What to organize: the current Stateboard repository
Destination: Dida/TickTick
Target location: a dedicated test list
Automatic refresh: not needed
```

If recurring automation is requested, the user must confirm both frequency and exact time first.

## Runtime Language

Use the user's request language for project tasks, task bodies, and run reports unless the user explicitly asks for bilingual output. If the request mixes languages and the destination write would be external, ask once before writing.

## Design Rules

- Do not default to 03:00 or any fixed automation time.
- Do not default to Dida/TickTick; discover the target tool and available connectors first.
- Distinguish "directly writable in the current Codex environment" from "possible through an official platform after configuration".
- Do not split historical context into many low-value tasks; default to one project task with 3-5 next actions.
- Prefer updating existing tasks over creating duplicates.
- If no connector exists, output copy/import instructions instead of calling private APIs.
- Do not pretend to read or write unavailable chats, project materials, task lists, calendars, or automation systems.

## File Structure

```text
SKILL.md
SKILL.zh.md
references/
  todo-app-capability-matrix.md
  todo-app-capability-matrix.zh.md
  integration-support.md
  integration-support.zh.md
  task-granularity-rubric.md
  task-granularity-rubric.zh.md
  top-skill-benchmark.md
  top-skill-benchmark.zh.md
templates/
  intake-questions.md
  intake-questions.zh.md
  sync-report-template.md
  sync-report-template.zh.md
  task-id-mapping-template.md
  task-id-mapping-template.zh.md
examples/
  stateboard-demo-dry-run.md
  stateboard-demo-dry-run.zh.md
```
