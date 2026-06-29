# Task Granularity Rubric

[中文](task-granularity-rubric.zh.md)

The main failure mode of this workflow is over-fragmentation. A project-state dashboard should make the next review easier, not create hundreds of stale tasks.

## Default Mode: Balanced Project Tasks

Use one task per active project/workstream.

Task body:

- positioning
- current progress
- priority
- next action
- blocker
- evidence date/source

Checklist:

- 3-5 next actions
- only actions that can be started without rereading the whole project

## Granularity Levels

### Compact Dashboard

Use when:

- user has many projects
- destination app is lightweight
- user wants a weekly overview

Shape:

- one summary task
- up to 5 active project tasks
- one parking-lot task

### Balanced Project Tasks

Use when:

- user wants a maintainable todo dashboard
- projects have clear next actions
- destination supports task descriptions/checklists

Shape:

- 1 summary task
- 1 task per active project
- 3-5 checklist items per task

### Detailed Next-Action Plan

Use when:

- user explicitly asks for execution planning
- a project is entering implementation
- target app supports subtasks or steps

Shape:

- project parent task
- 5-12 next actions
- separate blocker/decision tasks only when an owner and decision are clear

## What Counts As A Task

Create a task when the item:

- has an owner or the user can act on it
- can be started in one sitting
- has a decision, verification, or deliverable
- would become stale if not tracked

Keep in description when the item is:

- background context
- past evidence
- product positioning
- warning/guardrail
- historical note
- vague desire without next action

## Project Priority

- P0: active this week, release/blocker pressure, direct user focus
- P1: important, needs ongoing decisions or verification
- P2: stable baseline, useful but lower-frequency
- P3: dormant/parking lot, keep context but no immediate action

## Limits

Default limits:

- P0: max 3 projects
- P1: max 5 projects
- P2/P3: summarize aggressively
- Checklist items per project: 3-5
- Avoid more than 12 visible active tasks unless the user asks for a detailed plan

## Idempotency

Use stable titles and store task IDs in the automation prompt or a local mapping file.

Stable title pattern:

```text
P1｜Project：Positioning
```

If the priority changes, update the title in place. Do not create a new task.

## Status Language

Use evidence-aware phrasing:

- `Verified:`
- `Current evidence:`
- `No new evidence; carrying forward previous state:`
- `Blocked:`
- `Needs confirmation:`

Do not write "Complete" unless the project/workstream is actually complete.
