---
name: stateboard-codex
description: Use when a user wants AI project context from Codex, ChatGPT, Claude, DeepSeek, WorkBuddy, local repos, project notes, chats, or selected context files organized into a Stateboard-style project dashboard and synced into todo, calendar, or collaboration tools such as TickTick/Dida, Feishu/Lark, DingTalk, WeCom, Microsoft To Do, Apple Reminders, or Google Calendar.
metadata:
  short-description: Sync AI project state into Stateboard
---

# Stateboard Codex

[English](SKILL.md)

把分散的 AI 项目上下文整理成可维护的 Stateboard：一个持续更新的项目状态板，并同步到用户偏好的待办、日程、文档或协作系统。

这个 skill 用于维护项目状态，不是普通 todo capture。它应产出少量 durable project tasks，每条任务包含当前状态、优先级、下一步、阻塞项和证据。

## 何时使用

当用户要求以下事项时使用：

- 梳理正在 Codex / ChatGPT 推进的项目
- 梳理 Claude / DeepSeek / WorkBuddy / 其他 AI 工具里的项目对话
- 同步到滴答清单 / TickTick / Dida / Microsoft To Do / Apple Reminders / Calendar / 其他待办软件
- 同步到飞书 / Lark、钉钉 / DingTalk、企业微信 / WeCom 等协作平台
- 自动把项目状态整理成任务
- 每日 / 每周更新项目清单
- 把 ChatGPT / Codex 上下文变成项目管理面板

不要把这个 skill 用于一次性提醒，例如“明天提醒我给 X 打电话”，除非用户同时要求整理项目上下文。

## 核心理念

输出不是“AI 写 todo”。

输出是：

```text
project evidence -> project judgment -> durable task dashboard -> optional scheduled refresh
```

## 必要 Intake

创建任务或 recurring automation 前，用普通语言询问缺失字段。不要默认 03:00 或任何固定时间。

面向用户的 intake：

1. 我想整理的内容：包括哪些对话、项目、文件夹、笔记、任务或粘贴材料？
2. 同步到：哪个 app 或输出格式接收项目状态板？
3. 目标位置：使用或创建哪个清单、项目、页面、数据库、日历或 Markdown 输出？
4. 自动更新：不需要，或明确的每日 / 每周频率和具体时间。
5. 只有需要时才确认详情级别：默认用平衡项目任务，除非用户要求紧凑总览或详细行动计划。

如果用户已经给了某个值，不要重复询问。多个值缺失时，用一条简短消息一起问。不要向普通用户暴露 `source scope`、`ProjectState`、`task id mapping` 等内部术语，除非用户正在配置自动化或调试幂等更新。

缺少时间时可使用这段话：

```text
你希望项目状态自动化在什么时间运行？建议选一个你不太会正在编辑的时间，比如 07:30、09:00、18:30 或 22:30。也可以改成每周固定时间。
```

## 运行语言

默认用用户请求语言回复，并把目标系统中的任务标题、任务正文和 run report 写成同一语言；只有用户明确要求时才输出双语。

- 英文请求 -> 英文项目任务、任务正文和 run report。
- 中文请求 -> 中文项目任务、任务正文和 run report。
- 中英混合请求 -> 跟随用户明确指定的语言；如果不明确且即将写入外部系统，先问一次。

## 来源访问边界

只使用当前可读取、可搜索、已连接工具可访问，或用户已提供的内容。不要暗示可以访问另一个 AI 产品的私有历史，除非用户粘贴、上传、连接或授权了这些数据。

如果请求的来源不可用，询问缺失材料，或继续输出明确标注的 partial view。

## Connector 发现

1. 识别目标 app。
2. 假设可写入前先搜索可用工具：
   - TickTick/Dida：搜索 `滴答清单 dida365 ticktick task project create update search`
   - Google Calendar：搜索 `google calendar event create update`
   - Feishu/Lark、DingTalk、WeCom：阅读 `references/integration-support.md`，区分真实任务同步、日程同步和仅通知同步。
   - Microsoft / Outlook / To Do：先搜索可用 connector；没有则使用 export/fallback。
   - Apple Reminders / Calendar：只有用户明确启用本地 automation 时才使用；否则提供可导入文本 / 日历 fallback。
3. 如果没有 connector，不使用私有 API。输出结构化 fallback：
   - Markdown task dashboard
   - CSV-like import table
   - calendar/reminder 创建说明
   - 只有官方或 App Store 文档公开时才使用 app-specific URL scheme
   - 明确说明没有发生外部写入

## 默认工作流

1. **建立事实层。**
   - 读取最小有用连续性材料：项目说明、当前状态文档、repo status、已有任务和近期证据。
   - 优先使用当前文件和已知 automation state，而不是过期 summary。
   - 区分已确认事实、假设、阻塞和开放问题。

2. **创建项目 inventory。**
   - 每个真实项目 / workstream 一行。
   - 记录 name、positioning、status、priority、next action、blocker、evidence date。
   - 不要把历史记录都变成任务。

3. **选择任务颗粒度。**
   - 默认：balanced project tasks。
   - 使用 `references/task-granularity-rubric.md`。
   - 大多数项目保留为一个父任务 + 3-5 个 checklist 项。
   - 低信号休眠项目放入单个 parking-lot 任务。

4. **映射到目标 app。**
   - 使用 `references/todo-app-capability-matrix.md`。
   - 保留稳定任务标题和 ID，支持幂等更新。
   - 使用 `codex-sync`、project slug、priority 等标签。
   - 除非用户明确说项目完成，否则同步时不要把项目任务标记完成。

5. **只有用户要求时才设置 automation。**
   - 使用用户确认过的 schedule。
   - 优先更新已有 automation，而不是创建重复 automation。
   - Automation prompt 必须包含：
     - 目标 app / 清单标识
     - 已有任务 ID mapping
     - source directories、项目说明或用户选择的上下文文件
     - update-not-duplicate 规则
     - 验证步骤
     - 运行语言规则
   - 如果当前环境无法创建 automation，提供可复制设置说明，不要声称已创建。

6. **验证。**
   - 写入后搜索 / fetch 目标系统中的关键任务。
   - 如果搜索索引延迟，依赖写入工具返回值，并说明搜索可能滞后。
   - 如果创建或更新了 automation，验证配置处于 active 且使用用户确认的 schedule。

## 优先级 Rubric

除非用户提供其他规则，否则使用：

- `P0`：本周活跃、高紧急度、用户当前关注、或有 release/blocker 压力。
- `P1`：重要的进行中项目，需要决策、验证或协调。
- `P2`：有价值但低频的稳定工作流。
- `P3`：parking lot，保留上下文，无立即动作。

保守映射到 app 优先级：

- P0/P1 -> 如果 app 只有少数级别，设为高优先级。
- P2 -> normal priority。
- P3 -> low priority 或无 due date。

## 任务形态

默认标题：

```text
P1｜项目名：一句话定位
```

默认正文：

```text
项目定位：
当前进展：
优先级：
风险 / 边界：
下一步建议：
证据：
```

默认 checklist：

```text
- 确认当前事实层
- 解决下一个决策
- 执行验证 / review
- 更新项目说明或 dashboard
```

根据用户请求语言翻译 label 和任务正文。

## Guardrails

- 不要声称市场排名，除非本轮真的检查了当前排名来源。
- 如果已有清单 / 任务可更新，不要重复创建。
- 不要把项目历史过度拆成几十个任务。
- 不要把 secrets、tokens、private keys、license keys、个人凭据或私有目标系统标识写进任务描述。
- 未确认时间和频率前，不要创建 recurring automation。
- 不要假装访问了不可用的 chats、tools、lists、calendars 或 automation systems。
- 执行项目状态同步时，不要修改项目代码。
- 不要因为 memory 里有归档 / 休眠项目，就把它们当成活跃项目。

## References

- `references/todo-app-capability-matrix.md`
- `references/integration-support.md`
- `references/task-granularity-rubric.md`
- `references/top-skill-benchmark.md`
- `templates/intake-questions.md`
- `templates/sync-report-template.md`
- `templates/task-id-mapping-template.md`
- `examples/stateboard-demo-dry-run.md`

## 输出摘要

完成后，用用户请求语言报告：

- 创建 / 更新了哪个目标
- 创建 / 更新任务数量
- 验证结果
- automation 名称、schedule 和状态，或“未创建 / 等待确认时间”
- 未解决的 connector 或权限限制
