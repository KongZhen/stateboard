# Stateboard Codex Skill 使用说明

[English](README.md)

这是 Stateboard 的第一个 Codex skill，用来把 Codex / ChatGPT / Claude / DeepSeek / WorkBuddy、本地仓库、聊天记录和项目说明里的项目上下文整理成持续更新的项目状态板，并同步到待办、日程或团队协作工具。

它只会整理当前环境能读取、搜索到，或用户已经提供的内容；如果看不到某些对话或项目资料，必须说明缺口，不能假装已经读取。

它支持的目标形态包括：

- 滴答清单 / TickTick / Dida MCP
- Microsoft To Do / Outlook / Windows Focus Sessions
- Apple Reminders / Apple Calendar
- 飞书任务 / 飞书日历 / 飞书机器人
- 钉钉待办 / 钉钉日程 / 钉钉机器人
- 企业微信日程 / 企业微信应用消息 / 群机器人
- 其他待办软件的 Markdown / CSV-like / URL Scheme fallback

## 安装

把整个目录复制到 Codex skills 目录，例如：

```bash
cp -R skills/stateboard-codex ~/.codex/skills/stateboard-codex
```

然后在 Codex 中使用：

```text
$stateboard-codex
```

## 快速开始

最小 dry-run：

```text
$stateboard-codex

我想整理的内容：当前 Stateboard 仓库
同步到：只输出 Markdown
目标位置：直接发给我
自动更新：不需要
```

最小 live sync：

```text
$stateboard-codex

我想整理的内容：当前 Stateboard 仓库
同步到：滴答清单
目标位置：一个单独的测试清单
自动更新：不需要
```

如果要创建 recurring automation，必须先由用户确认频率和具体时间。

## 运行语言

默认使用用户请求语言生成项目任务、任务正文和 run report；只有用户明确要求时才输出双语。中英混合且即将外部写入时，先问一次再写入。

## 关键设计

- 不默认凌晨 3 点；必须询问用户自动化时间。
- 不默认滴答清单；先发现目标工具和可用 connector。
- 区分“当前 Codex 环境直接可写”和“官方开放平台可接但需要配置凭据/应用”。
- 不把历史上下文拆成一堆垃圾任务；默认一项目一任务，3-5 个下一步。
- 自动化优先更新已有任务，避免重复创建。
- 没有 connector 时输出可复制/可导入方案，不调用私有接口。
- 看不到的 AI 对话、项目资料或目标系统，不假装已经读取或写入。

## 文件结构

```text
SKILL.md
SKILL.zh.md
references/
  todo-app-capability-matrix.md
  todo-app-capability-matrix.zh.md
  integration-support.md
  integration-support.zh.md
  task-granularity-rubric.md
  task-granularity-rubric.zh.md
  top-skill-benchmark.md
  top-skill-benchmark.zh.md
templates/
  intake-questions.md
  intake-questions.zh.md
  sync-report-template.md
  sync-report-template.zh.md
  task-id-mapping-template.md
  task-id-mapping-template.zh.md
examples/
  stateboard-demo-dry-run.md
  stateboard-demo-dry-run.zh.md
```
