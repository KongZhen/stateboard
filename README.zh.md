# Stateboard

[English](README.md)

把 AI 工作上下文变成持续更新的项目状态板。

Stateboard 把分散在 AI 对话、项目文件、项目说明、待办和验证结果里的工作上下文，整理成持续更新的项目状态板，并同步到用户已经使用的待办、日程或团队协作工具。

> 当前状态：alpha。V1 先提供可复制 prompt 和 Codex skill 两种入口，核心库与 adapters 会从真实同步场景中逐步抽象。

## 它解决什么问题

你可能同时在 Codex、ChatGPT、Claude、DeepSeek、WorkBuddy、本地仓库、Notion、日历和待办软件中推进多个项目。普通 todo 工具通常只记录“要做什么”，但项目真实状态还需要判断：

- 哪些项目仍然活跃，哪些只是历史上下文
- 当前进展来自哪些证据
- 下一步是实现、验证、决策、发布，还是等待外部输入
- 优先级是否需要变化
- 目标系统里应更新已有任务，还是创建新任务

Stateboard 的目标不是把所有聊天记录拆成任务，而是维护一层项目状态。

```text
AI conversations / project files / project notes
-> evidence-based project state
-> durable project tasks
-> todo, calendar, docs, or team tools
-> optional scheduled refresh
```

## 两种入口

### 1. Prompt：零安装快速开始

复制 [prompts/stateboard-sync-prompt.zh.md](prompts/stateboard-sync-prompt.zh.md)，一次性填好四项：

- 我想整理的内容
- 同步到
- 目标位置
- 自动更新

适合：

- 先验证 Stateboard 是否适合自己的工作流
- 在 Codex / ChatGPT / Claude / DeepSeek / WorkBuddy 等环境里手动运行
- 没有安装 skill 或 connector 时生成 Markdown fallback

### 2. Skill：可复现工作流

安装 [skills/stateboard-codex](skills/stateboard-codex/)：

```bash
cp -R skills/stateboard-codex ~/.codex/skills/stateboard-codex
```

在 Codex 中使用：

```text
$stateboard-codex

我想整理的内容：当前项目
同步到：只输出 Markdown
目标位置：直接发给我
自动更新：不需要
```

适合：

- 长期复用同一套项目状态规则
- 跨会话复用
- 保持更严格的 guardrails
- 后续接入真实任务系统和定时刷新

## 当前支持策略

Stateboard 会区分“当前环境直接可写”和“官方 API 可接入但需要配置”。不要把这两种情况混成一句“支持”。

## 运行语言

Prompt 和 skill 默认跟随用户请求语言：

- 英文请求 -> 英文项目任务和 run report。
- 中文请求 -> 中文项目任务和 run report。
- 中英混合请求 -> 跟随用户明确指定的语言；如果不明确且即将写入外部系统，先问一次。
- 只有用户明确要求时才输出双语。

| 目标 | 当前建议 |
|---|---|
| 滴答清单 / Dida / TickTick | 当前 Codex 环境中可作为真实任务面板验证 |
| Google Calendar | 适合创建项目 review block，不是任务数据库 |
| Notion | 适合项目 dashboard 或文档化状态页 |
| 飞书 / Lark | 适合作为企业版真实任务系统 adapter |
| 钉钉 / DingTalk | 适合企业工作待办，但依赖组织应用和权限 |
| 企业微信 / WeCom | 优先作为通知和日程层，不建议单独作为主任务库 |
| 其他工具 | 先输出 Markdown / CSV-like / 复制导入方案 |

更完整的判断见 [docs/integration-matrix.zh.md](docs/integration-matrix.zh.md)。

## 关键规则

- 先建立事实层，再判断项目状态和优先级。
- 默认一个真实项目对应一条 durable project task，并附 3-5 个下一步。
- 写入前搜索已有任务，优先更新同一任务，避免重复创建。
- 不把历史记忆拆成大量低价值任务。
- 没有明确频率和具体时间时，不创建 recurring automation。
- 不把 webhook 通知描述成完整任务系统。
- 不写入 token、webhook、license key、私有凭据或用户私有任务系统 ID。

## 项目结构

```text
prompts/
  stateboard-sync-prompt.md
  stateboard-sync-prompt.zh.md
  stateboard-automation-prompt.md
  stateboard-automation-prompt.zh.md

skills/stateboard-codex/
  SKILL.md
  SKILL.zh.md
  README.md
  README.zh.md
  references/
  templates/
  examples/

docs/
  product-definition.md
  product-definition.zh.md
  integration-matrix.md
  integration-matrix.zh.md
  testing.md
  testing.zh.md
  index.html
  index.zh.html

packages/
  core/
  adapters/
```

## 本地验证

最小 dry-run：

```text
我想整理的内容：当前项目
同步到：只输出 Markdown
目标位置：直接发给我
自动更新：不需要
```

真实写入验证建议先用单独测试清单或页面，并检查：

- 是否只创建或更新一条项目状态任务
- 搜索能否取回同一任务
- 再次运行是否更新同一任务而不是重复创建
- 输出报告是否说明写入、验证、阻塞和自动化状态

## 文档

- [产品定义](docs/product-definition.zh.md)
- [Prompt 入口说明](docs/prompt-template.zh.md)
- [测试](docs/testing.zh.md)
- [集成矩阵](docs/integration-matrix.zh.md)
- [路线图](docs/roadmap.zh.md)

## 路线图

- Phase 1：prompt 与 `stateboard-codex` skill 双入口验证
- Phase 2：抽象 `ProjectState`、`TaskSink`、`CalendarSink`、`NotificationSink`
- Phase 3：实现 Dida/TickTick、Notion、Google Calendar 和 Feishu adapters
- Phase 4：沉淀 CLI、examples 和更多目标系统验证

## 许可证

MIT. See [LICENSE](LICENSE).
