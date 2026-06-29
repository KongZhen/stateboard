# Top Skill Benchmark

[中文](top-skill-benchmark.zh.md)

Use this checklist to make the skill feel like a strong reusable agent capability rather than a one-off script.

## 1. Narrow Trigger

Good skills are precise.

This skill should trigger on "project context -> todo dashboard", not every reminder request.

## 2. Mandatory Intake Before Side Effects

The skill must ask before creating:

- destination app/list
- automation time/frequency
- source scope
- granularity

It may create a draft plan before asking, but not recurring automation.

## 3. Connector-Aware Execution

The skill should not assume TickTick/Dida.

It should:

- discover available MCP tools
- use official connectors first
- gracefully fall back to importable output
- state capability limits

## 4. Idempotent Writes

Top skills avoid duplicate clutter.

Requirements:

- search before creating
- update known task IDs
- keep a mapping in automation prompt or local state
- create new tasks only for new high-signal projects

## 5. Evidence Quality

Every project status should be grounded in a source:

- memory summary
- repo file
- project note/current state doc
- recent task result
- automation run result

If no fresh evidence exists, say so.

## 6. Granularity Control

A good skill knows when not to create tasks.

Rules:

- one project = one task by default
- no historical note tasks
- parking-lot dormant projects
- max 3-5 next actions per project unless asked

## 7. Verification

After writing:

- search/fetch key tasks
- verify completed test task only if a test task was intentionally created
- verify automation status and schedule
- report indexing delays separately from write failures

## 8. Cross-App Portability

The skill should preserve the semantic model:

```text
Project -> Status -> Priority -> Next actions -> Blockers -> Evidence
```

Then map to each app's available structure:

- TickTick/Dida: project/list + tasks + tags + priority + checklist
- Microsoft To Do: list + task + steps + reminders
- Apple Reminders: list + reminders + subtasks + tags/smart lists
- Calendar: review block, not task database
- Lightweight apps: compact copy-ready tasks

## 9. Automation Safety

Recurring automation should:

- have a human-confirmed schedule
- update in place
- avoid secret leakage
- not modify project code
- produce short run reports

## 10. Installable Packaging

Deliver as a complete folder:

```text
skill-name/
  SKILL.md
  references/
  templates/
```

Keep the root `SKILL.md` concise and put market/app details in references.
