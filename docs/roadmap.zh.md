# Roadmap

[English](roadmap.md)

## Phase 1: 可复现入口

- 保留并测试两种入口：可复制 prompt 与 `stateboard-codex` skill。
- 为 prompt 入口提供普通用户只需填写一次的 `prompts/stateboard-sync-prompt.md`；automation prompt 只作为高级实现模板保留。
- 保持 `skills/stateboard-codex/` 可安装。
- 外部写入前先提供 Markdown dry-run 测试。
- 在 `docs/testing.md` 中记录可选 live-sync 测试方式。
- automation 必须等待用户确认频率和具体运行时间。

## Phase 2: Core Schema

- 抽象 `ProjectState`。
- 抽象 `TaskSink`、`CalendarSink`、`NotificationSink`。
- 定义幂等更新规则和 ID 映射。
- 定义任务粒度 rubric。

## Phase 3: Adapters

- Dida / TickTick adapter。
- Google Calendar review block。
- Notion dashboard。
- Feishu task + reminder + bot card 原型。

## Phase 4: 开源分发

- 使用 MIT license。
- 公开文档以英文主版为准，并保留完整中文 `.zh.md` 镜像。
- 提供中英文 GitHub Pages 单页介绍页。
- 公开示例保持泛化，不暴露私人项目历史。
- core schema 和首批 adapters 稳定前保持 alpha 标记。
