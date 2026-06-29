# Stateboard Product Definition

[中文](product-definition.zh.md)

## One Line

Turn AI work context into a project-status board that can refresh every day.

Tagline:

```text
Turn AI work context into a living project board.
```

## Problem

People move projects across Codex, ChatGPT, local repositories, design tools, Notion, calendars, and todo apps. Real progress is scattered across conversations, files, automation output, test results, and memory.

A normal todo tool can store "what to do", but it cannot automatically judge:

- which projects are genuinely active
- which items are only historical context
- whether current progress has evidence
- whether the next step is code, verification, a decision, release, or waiting for input
- how priority should change

Stateboard turns that scattered state into a maintainable project board and syncs it to the systems users already use.

## Core Flow

```text
context intake
-> evidence normalization
-> project state judgment
-> task granularity control
-> destination mapping
-> idempotent sync
-> scheduled refresh
```

## V1 Shape

V1 does not start with a complex framework or standalone service. It keeps two entry points:

1. **Prompt entry**: zero-install, copyable into Codex / ChatGPT / other AI tools for manual runs or automation setup.
2. **Skill entry**: installable and versionable, better for long-term reuse across sessions and stronger guardrails.

Both entry points must follow the same Stateboard rules:

- Establish the truth layer before judging project state and priority.
- Discover target-system capability before assuming a connector exists.
- Search before writing; update the same task when possible.
- Control task granularity; do not split historical memory into many low-value tasks.
- Confirm frequency and exact time before creating recurring automation.
- Output a short run report after every run.
- Follow the user's request language unless bilingual output is explicitly requested.

Current skill shape:

```text
stateboard-codex
  -> read project truth layer
  -> produce ProjectState
  -> map to destination project-status tasks
  -> verify write and idempotent update
```

The prompt template lives at `prompts/stateboard-sync-prompt.md`. `prompts/stateboard-automation-prompt.md` is an advanced template for agents after the user has confirmed automation timing.

`packages/core/` and `packages/adapters/` are placeholders for later extraction. Do not design complex interfaces before real usage proves the shape.

## Why Not Just A Prompt

A single prompt already proved that organizing Codex / ChatGPT context and syncing it to Dida/TickTick is feasible. Stateboard keeps the prompt form because it is the lowest-friction entry point and works well for user-configured automation.

`stateboard-codex` is valuable because it turns one successful prompt into a reproducible, constrained, versioned workflow. The skill preserves behaviors that are easy to lose when a prompt is copied or modified:

- evidence-first project-state judgment
- connector discovery before writes
- search-and-update before create
- task granularity control
- automation time confirmation
- short verification report
- runtime language discipline

If the user only needs a temporary sync, a strong prompt is enough. The V1 goal is to make the same project-state rules available through both a low-friction prompt and a maintainable skill.

## MVP

Phase 1 focuses on one reliable loop:

1. Extract project state from Codex / ChatGPT related context.
2. Produce positioning, current progress, priority, next steps, blockers, and evidence.
3. Default to one task per project, with 3-5 next-action checklist items.
4. Sync to Dida/TickTick MCP and verify search/update without duplicates.
5. Add daily or weekly refresh later, only after asking the user for frequency and exact time.

The first proof of work is a reproducible dry-run, followed by an optional live sync into a user-approved test destination.

## Non-Goals

- Not a generic one-off reminder bot.
- Not a tool that turns every chat message into a task.
- Not an automation that assumes a default run time.
- Not a webhook notification wrapper pretending to be a full task system.
- Not a place to store or sync secrets, tokens, license keys, or personal credentials.

## Key Objects

```text
ProjectState
  name
  positioning
  status
  priority
  next_actions
  blockers
  evidence
  source_scope
  updated_at

TaskSink
  create_project
  find_existing_task
  create_task
  update_task
  verify_task

CalendarSink
  create_review_event
  update_review_event

NotificationSink
  send_digest
```

## Default Granularity

Default mode is balanced project tasks:

- One real project maps to one parent task.
- The task body records positioning, progress, priority, risks, and evidence.
- The checklist keeps 3-5 next actions.
- Low-activity projects go to the parking lot instead of becoming separate task clusters.
