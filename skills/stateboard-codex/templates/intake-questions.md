# Intake Questions

[中文](intake-questions.zh.md)

Use these questions before creating tasks or automations. Translate them into the user's request language before sending.

## Minimal Intake

```text
I need to confirm five settings before writing to the destination:

1. What should I organize? For example: recent AI conversations you provide or I can read, the current project, a project folder, existing todos, or pasted chat records.
2. Where should I sync it? For example: Dida/TickTick, Notion, Google Calendar, Feishu/Lark, DingTalk, WeCom, or Markdown only.
3. What is the target location? For example: a list, page, database, or calendar. If it does not exist, I can create it when the connector allows it.
4. Do you need automatic refresh? Not needed, daily at a specific time, or weekly at a specific time.
5. Optional: do you want a compact overview, balanced project tasks, or a detailed next-action plan? If you do not specify, I will use balanced project tasks.
```

## Time Confirmation

```text
What time should the automation run?

Common choices:
- 07:30: before the workday starts
- 09:00: at workday startup
- 18:30: before end-of-day wrap-up
- 22:30: after evening review
- Monday 09:00 every week: weekly planning instead of daily refresh
```

## Granularity Confirmation

```text
I recommend "balanced project tasks" by default:

- 1 task per active project
- 3-5 next steps per task
- low-frequency projects go into a parking lot

If you want something lighter, I can produce only an overview. If you are ready to execute one project, I can expand that project into a detailed next-action plan.
```
