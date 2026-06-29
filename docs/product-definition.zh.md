# Stateboard 产品定义

[English](product-definition.md)

## 一句话

把 AI 工作上下文，变成每天更新的项目状态板。

英文副标题：

```text
把 AI 工作上下文变成持续更新的项目状态板。
```

## 解决的问题

用户在 Codex、ChatGPT、本地仓库、设计工具、Notion、日历和待办软件之间推进多个项目。真实进展分散在对话、文件、自动化、测试结果和记忆里。

普通 todo 工具只能记录“要做什么”，但不能自动判断：

- 哪些项目是真的正在推进
- 哪些只是历史上下文
- 当前进展是否有证据
- 下一步是写代码、验证、决策、发布，还是等待外部输入
- 优先级应该如何变化

Stateboard 的目标是把这些分散状态整理成可维护的项目面板，并同步到用户已经使用的系统。

## 核心流程

```text
context intake
-> evidence normalization
-> project state judgment
-> task granularity control
-> destination mapping
-> idempotent sync
-> scheduled refresh
```

## V1 形态

V1 先不做复杂框架或独立服务，同时保留两种入口：

1. **Prompt 入口**：零安装，适合用户复制到 Codex / ChatGPT 里快速运行或配置 automation。
2. **Skill 入口**：可安装、可版本化，适合跨会话长期复用和更严格的 guardrails。

两种入口都必须遵守同一套 Stateboard 规则：

- 先建立事实层，再判断项目状态和优先级。
- 先发现目标系统能力，不默认某个 connector。
- 写入前搜索已有任务，优先更新同一任务，避免重复创建。
- 控制任务颗粒度，不把历史记忆拆成大量低价值任务。
- 创建 recurring automation 前必须确认频率和时间。
- 每次运行后输出简短 report，记录写入、验证、阻塞和后续动作。

Skill 入口的当前形态：

```text
stateboard-codex
  -> 读取项目事实层
  -> 生成 ProjectState
  -> 映射成目标系统里的项目状态任务
  -> 验证写入和幂等更新
```

Prompt 入口的当前用户模板见 `prompts/stateboard-sync-prompt.md`。`prompts/stateboard-automation-prompt.md` 是高级模板，供 agent 在用户已确认自动更新时间后生成 Codex automation。

`packages/core/` 和 `packages/adapters/` 暂时只保留方向，不在没有真实使用证据前抽象复杂接口。核心判断先沉淀在 prompt template、`stateboard-codex` 的工作流、references 和测试清单中。

## 为什么不是一段 Prompt

一段 prompt 已经可以验证“整理 Codex / ChatGPT 上下文并同步到滴答清单”这件事可行。Stateboard 会保留 prompt 形态，因为它是最低门槛入口，也适合用户直接配置 Codex automation。

`stateboard-codex` 的价值不在于证明一次性能力，而在于把这次成功沉淀成可复现、可约束、可版本化的工作流。Skill 需要固化这些 prompt 容易遗漏或在复制中漂移的行为：

- 先建立事实层，再判断项目状态和优先级。
- 先发现目标系统能力，不默认某个 connector。
- 写入前搜索已有任务，优先更新同一任务，避免重复创建。
- 控制任务颗粒度，不把历史记忆拆成大量低价值任务。
- 创建 recurring automation 前必须确认频率和时间。
- 每次运行后输出简短 report，记录写入、验证、阻塞和后续动作。

如果只是临时同步一次，一段高质量 prompt 足够。Stateboard 的 v1 目标是让同一套项目状态同步规则同时具备 prompt 的低门槛和 skill 的可维护性。

## MVP

第一阶段只做一个可靠闭环：

1. 从 Codex / ChatGPT 相关上下文中提取项目状态。
2. 为项目生成定位、当前进展、优先级、下一步、阻塞项和证据。
3. 默认一项目一任务，附 3-5 个下一步 checklist。
4. 同步到滴答清单 MCP，并验证搜索和更新不会重复创建。
5. 后续可建立每日或每周自动更新任务，但必须先询问用户频率和时间。

第一条 proof of work 是可复现的 dry-run；只有用户确认目标系统和写入权限后，才执行可选 live sync。

## 非目标

- 不做普通的一次性提醒机器人。
- 不把所有聊天记录都转成任务。
- 不默认某个时间自动运行。
- 不把通知 webhook 伪装成完整任务管理系统。
- 不存储或同步密钥、token、license key、个人凭据。

## 关键对象

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

## 默认任务粒度

默认使用 balanced 模式：

- 一个真实项目对应一个父任务。
- 父任务正文记录项目定位、进展、优先级、风险、证据。
- checklist 保留 3-5 个下一步。
- 低活跃项目进入 parking lot，不拆成多个任务。
