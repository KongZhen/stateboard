# Todo App 能力矩阵

[English](todo-app-capability-matrix.md)

这份 reference 用来把项目状态同步 workflow 适配到常见中文 todo app，以及 Windows/macOS 内置提醒系统。

下面的“前 5”应被视为实用 benchmark 集合，不是精确市场份额排名，除非当前运行中验证了实时排名来源。

当前已验证的 connector/API 状态另见：

- `integration-support.md`

## 面向中国用户的 Todo Benchmarks

### 1. 滴答清单 / Dida / TickTick

为什么重要：

- 当 MCP 可用时，这是本 skill 最强的适配目标。
- 官方 MCP 支持 AI assistant 读取、创建和管理任务。
- 产品支持任务、清单 / 文件夹、标签、优先级、提醒、日历视图、番茄、习惯、笔记、协作和多端同步。

最佳同步形态：

- 一个项目 / 清单作为 Codex dashboard。
- 每个项目一条 durable task。
- 标签：`codex-sync`、项目 slug、优先级。
- 使用稳定任务 ID 和批量更新。

风险：

- 创建后搜索索引可能延迟；即时验证优先依赖写入返回的任务 ID。

Sources:

- https://help.dida365.com/articles/7438132116019216384
- https://apps.apple.com/us/app/id626144601?l=zh-Hans-CN&platform=mac
- https://dida365.com/

### 2. Todo清单

为什么重要：

- 面向中国用户的 GTD/todo 产品，支持跨端同步和番茄定位。
- 可作为“任务清单 + 专注”workflow 的 benchmark。

最佳同步形态：

- 使用项目级任务和简短下一步列表。
- 如果没有 MCP/API connector，生成可导入 Markdown 或可复制任务。

风险：

- 没有官方 connector 前，不要假设可以直接写入。

Sources:

- https://todo.evestudio.cn/
- https://sj.qq.com/appdetail/com.eve.todolist

### 3. 极简待办 / MinimaList

为什么重要：

- 轻量个人任务 / 提醒 app。
- 支持 todo lists、reminders、shared lists、widgets、calendar sync、Pomodoro，以及 App Store 文档化 URL Scheme。

最佳同步形态：

- 紧凑模式比详细项目 dashboard 更合适。
- 如果用户明确选择此 app 且在 Apple 平台上，可以考虑 URL Scheme 创建单个任务。

风险：

- URL Scheme 需要编码，且不是完整 sync API；只用于明确的小规模写入。

Sources:

- https://apps.apple.com/cn/app/id993066159

### 4. 专注清单 / Focus To-Do

为什么重要：

- 结合番茄、任务清单、提醒、子任务、重复任务、笔记、统计和 Android/iOS/Windows/Mac 跨端同步。
- 是任务执行和专注 session planning 的好 benchmark。

最佳同步形态：

- 项目任务应偏执行导向。
- 只有当用户要执行计划时，才增加估算专注块。

风险：

- 如果没有 connector，不要自动化私有 app 状态。输出清晰计划即可。

Sources:

- https://www.focustodo.cn/?lang=zh_CN
- https://play.google.com/store/apps/details?id=com.superelement.pomodoro&hl=zh

### 5. 敬业签

为什么重要：

- 在中文用户中有强提醒 / 笔记定位。
- 支持 notes、todo、提醒、多端同步、微信 / 钉钉 / SMS / 电话 / 邮件等提醒方式、时间轴 / 历史、分类、桌面 / 移动 / Web 使用。

最佳同步形态：

- 适合提醒密集型项目状态和 recurring review prompt。
- 任务正文保持简短；上下文使用 notes/history。

风险：

- 把它视为提醒 / 笔记系统，不一定是结构化项目任务 API。

Sources:

- https://www.jingyeqian.com/

## Windows 内置 / Microsoft Stack

### Microsoft To Do

能力：

- 截止日期、提醒、重复任务、自然语言日期 / 提醒识别、清单、steps。
- Outlook 可以管理带截止日期和提醒的 To Do tasks。

最佳同步形态：

- 使用 lists 和带 steps 的 tasks。
- 只有真正有时间约束的下一步才使用 reminders。
- 默认不要把 To Do tasks 伪装成 calendar events。

Sources:

- https://support.microsoft.com/en-us/todo/add-due-dates-and-reminders-in-microsoft-to-do
- https://support.microsoft.com/en-us/todo/smart-due-date-reminder-recognition-in-microsoft-to-do
- https://support.microsoft.com/en-us/outlook/calendar/manage-tasks-with-to-do-in-outlook

### Windows Focus Sessions

能力：

- Windows Clock Focus sessions 支持专注计时、勿扰行为和 Microsoft To Do 集成。

最佳同步形态：

- 用 To Do tasks 作为任务源；用 Focus Sessions 做执行块。
- 不要把 Focus Sessions 当成存储层。

Sources:

- https://support.microsoft.com/en-us/windows/focus-stay-on-task-without-distractions-in-windows-cbcc9ddb-8164-43fa-8919-b9a2af072382
- https://www.microsoft.com/en-us/windows/tips/focus-sessions

### Outlook Calendar

能力：

- Calendar events、event reminders、recurring events、单独 reminders window、Outlook 中的 To Do/task reminders。

最佳同步形态：

- 用 calendar events 表达 review blocks、会议和基于时间的计划。
- 用 To Do 表达任务状态。

Sources:

- https://support.microsoft.com/en-us/outlook/calendar/add-or-delete-notifications-or-reminders-in-outlook
- https://support.microsoft.com/en-us/outlook/training/use-calendar-categories-and-reminders-in-outlook

## macOS 内置 / Apple Stack

### Apple Reminders

能力：

- Lists、tags、Smart Lists、subtasks、templates、scheduled reminders。
- Calendar 可以显示 scheduled Reminders。

最佳同步形态：

- 一个 list 作为项目 dashboard。
- 每个项目一个 reminder，subtasks 表示下一步。
- Tags 可表示优先级和项目域。

Sources:

- https://support.apple.com/guide/reminders/create-custom-smart-lists-remnfec66479/mac
- https://support.apple.com/guide/reminders/add-subtasks-to-reminders-remn32a9622b/mac
- https://support.apple.com/guide/reminders/tag-reminders-remn45640f4f/mac
- https://support.apple.com/guide/reminders/use-reminder-list-templates-remn29caf6e1/mac

### Apple Calendar

能力：

- Events、repeating events、alerts、travel time、多账号同步。
- Reminders 中已安排时间的提醒可以显示在 Calendar。

最佳同步形态：

- 用 Calendar 表示 recurring review blocks。
- 用 Reminders 表示项目 / 任务状态。

Sources:

- https://support.apple.com/guide/calendar/set-up-or-delete-a-repeating-event-icl1018/mac
- https://support.apple.com/guide/calendar/use-reminders-icl873b9a527/mac
- https://support.apple.com/guide/calendar/add-location-and-travel-time-to-events-icl43600/mac

## Connector 策略

按这个顺序选择：

1. Native MCP / app connector。
2. 官方 API。
3. 官方 URL Scheme / Shortcuts / calendar event creation。
4. 可导入 Markdown / CSV-like 输出。
5. 手动设置说明。

不要为用户抓取或逆向私有 app API。
