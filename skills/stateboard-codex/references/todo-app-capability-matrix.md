# Todo App Capability Matrix

[中文](todo-app-capability-matrix.zh.md)

This reference helps adapt the project-state sync workflow to common Chinese todo apps and built-in Windows/macOS reminder systems.

The "top 5" below should be treated as a practical benchmark set, not a precise market-share ranking, unless the current run verifies a live ranking source.

For the current verified connector/API status, also read:

- `integration-support.md`

## Domestic / China-Facing Todo Benchmarks

### 1. 滴答清单 / Dida / TickTick

Why it matters:

- Strongest fit for this skill when MCP is available.
- Official MCP supports AI assistants reading, creating, and managing tasks.
- Product supports tasks, lists/folders, tags, priority, reminders, calendar view, Pomodoro, habits, notes, collaboration, and multi-platform sync.

Best sync shape:

- One project/list for the Codex dashboard.
- One durable task per project.
- Tags: `codex-sync`, project slug, priority.
- Use stable task IDs and batch updates.

Risk:

- Search indexing may lag after creation; rely on returned task IDs for immediate verification.

Sources:

- https://help.dida365.com/articles/7438132116019216384
- https://apps.apple.com/us/app/id626144601?l=zh-Hans-CN&platform=mac
- https://dida365.com/

### 2. Todo清单

Why it matters:

- China-facing GTD/todo product with cross-platform sync and Pomodoro positioning.
- Useful benchmark for "task list + focus" workflows.

Best sync shape:

- Use project-level tasks and short next-action lists.
- If no MCP/API connector exists, generate importable Markdown or copy-ready tasks.

Risk:

- Do not assume direct write access without an official connector.

Sources:

- https://todo.evestudio.cn/
- https://sj.qq.com/appdetail/com.eve.todolist

### 3. 极简待办 / MinimaList

Why it matters:

- Lightweight personal task/reminder app.
- Supports todo lists, reminders, shared lists, widgets, calendar sync, Pomodoro, and an App Store documented URL Scheme.

Best sync shape:

- Compact mode works better than detailed project dashboards.
- If the user explicitly chooses this app and is on Apple platforms, URL Scheme creation can be considered for single-task creation.

Risk:

- URL Scheme content needs encoding and is not a full sync API; use it only for explicit, small writes.

Sources:

- https://apps.apple.com/cn/app/id993066159

### 4. 专注清单 / Focus To-Do

Why it matters:

- Combines Pomodoro, task list, reminders, subtasks, repeat tasks, notes, reporting, and cross-platform sync across Android/iOS/Windows/Mac.
- Good benchmark for task execution and focus-session planning.

Best sync shape:

- Keep project tasks execution-oriented.
- Add estimated focus blocks only when the user wants execution planning.

Risk:

- If no connector is available, do not automate private app state. Export a clear plan.

Sources:

- https://www.focustodo.cn/?lang=zh_CN
- https://play.google.com/store/apps/details?id=com.superelement.pomodoro&hl=zh

### 5. 敬业签

Why it matters:

- Strong reminder/notes positioning for Chinese users.
- Supports notes, todo items, reminders, multi-device sync, WeChat/DingTalk/SMS/phone/email style reminders, timeline/history, categories, and desktop/mobile/web usage.

Best sync shape:

- Good for reminder-heavy project status and recurring review prompts.
- Keep task bodies concise; use notes/history for context.

Risk:

- Treat as reminder/notes system, not necessarily a structured project-task API.

Sources:

- https://www.jingyeqian.com/

## Windows Built-In / Microsoft Stack

### Microsoft To Do

Capabilities:

- Due dates, reminders, repeating tasks, natural-language date/reminder recognition, lists, and steps.
- Outlook can manage To Do tasks with due dates and reminders.

Best sync shape:

- Use lists and tasks with steps.
- Use reminders only for truly time-bound next actions.
- Avoid pretending To Do tasks are calendar events by default.

Sources:

- https://support.microsoft.com/en-us/todo/add-due-dates-and-reminders-in-microsoft-to-do
- https://support.microsoft.com/en-us/todo/smart-due-date-reminder-recognition-in-microsoft-to-do
- https://support.microsoft.com/en-us/outlook/calendar/manage-tasks-with-to-do-in-outlook

### Windows Focus Sessions

Capabilities:

- Windows Clock Focus sessions support focus timers, do-not-disturb behavior, and Microsoft To Do integration.

Best sync shape:

- Use To Do tasks as the task source; use Focus Sessions for execution blocks.
- Do not use Focus Sessions as the storage layer.

Sources:

- https://support.microsoft.com/en-us/windows/focus-stay-on-task-without-distractions-in-windows-cbcc9ddb-8164-43fa-8919-b9a2af072382
- https://www.microsoft.com/en-us/windows/tips/focus-sessions

### Outlook Calendar

Capabilities:

- Calendar events, event reminders, recurring events, separate reminders window, To Do/task reminders in Outlook.

Best sync shape:

- Use calendar events for review blocks, meetings, and time-based planning.
- Use To Do for task state.

Sources:

- https://support.microsoft.com/en-us/outlook/calendar/add-or-delete-notifications-or-reminders-in-outlook
- https://support.microsoft.com/en-us/outlook/training/use-calendar-categories-and-reminders-in-outlook

## macOS Built-In / Apple Stack

### Apple Reminders

Capabilities:

- Lists, tags, Smart Lists, subtasks, templates, scheduled reminders.
- Calendar can display scheduled Reminders.

Best sync shape:

- Use one list for project dashboard.
- One reminder per project, subtasks for next actions.
- Tags can model priority and project domains.

Sources:

- https://support.apple.com/guide/reminders/create-custom-smart-lists-remnfec66479/mac
- https://support.apple.com/guide/reminders/add-subtasks-to-reminders-remn32a9622b/mac
- https://support.apple.com/guide/reminders/tag-reminders-remn45640f4f/mac
- https://support.apple.com/guide/reminders/use-reminder-list-templates-remn29caf6e1/mac

### Apple Calendar

Capabilities:

- Events, repeating events, alerts, travel time, multi-account sync.
- Scheduled reminders from Reminders can be shown in Calendar.

Best sync shape:

- Use Calendar for recurring review blocks.
- Use Reminders for project/task state.

Sources:

- https://support.apple.com/guide/calendar/set-up-or-delete-a-repeating-event-icl1018/mac
- https://support.apple.com/guide/calendar/use-reminders-icl873b9a527/mac
- https://support.apple.com/guide/calendar/add-location-and-travel-time-to-events-icl43600/mac

## Connector Strategy

Use this order:

1. Native MCP/app connector.
2. Official API.
3. Official URL Scheme / Shortcuts / calendar event creation.
4. Importable Markdown/CSV-like output.
5. Manual setup instructions.

Never scrape or reverse-engineer private app APIs for another user.
