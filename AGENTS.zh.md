# AGENTS.md

[English](AGENTS.md)

公开项目文档以英文主版为准。所有面向用户的公开 Markdown 文档都应在同目录保留完整中文镜像，使用 `.zh.md` 后缀。

进入本项目时，先读：

1. `README.md`
2. `docs/product-definition.md`
3. `docs/integration-matrix.md`
4. `docs/testing.md`
5. `skills/stateboard-codex/SKILL.md`

项目目标是把 AI 工作上下文同步成项目状态板。不要把它简化成普通 todo 机器人。

默认原则：

- 先建立事实层，再判断任务和优先级。
- 区分真实任务同步、日程同步和通知同步。
- 不在用户未确认频率和具体时间时创建自动化。
- 不把历史记忆拆成大量低价值任务。
- 不把 webhook 通知描述成完整任务系统。
- 运行时输出语言跟随用户请求语言；只有用户明确要求时才输出双语。
