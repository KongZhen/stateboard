# 集成矩阵

[English](integration-matrix.md)

本文记录 Stateboard 对 todo、日程、文档和协作目标系统的公开接入模型。

关键原则：不要只说“支持某某平台”，必须说明支持层级。

## 支持层级

```text
Tier 1: 当前运行环境有直接 connector
Tier 2: 官方 API 可接入，但需要应用、权限、token 或自定义 connector
Tier 3: 通知 / 日程层接入，不是完整任务数据库
Tier 4: 导出 / 复制 / Markdown fallback
```

## 常见目标系统

| 目标 | 层级 | 用途 |
|---|---:|---|
| 滴答清单 / Dida / TickTick | Tier 1 或 2 | 有 MCP 或官方 connector 时，适合作为个人主任务板 |
| Google Calendar | Tier 1 或 2 | 项目复盘时间块和提醒，不是任务数据库 |
| Notion | Tier 1 或 2 | 项目 dashboard 或文档化状态页 |
| Codex Automations | Runtime feature | 定时刷新；不是任务目标系统 |

## 企业协作平台

| 平台 | 推荐角色 | 判断 |
|---|---|---|
| 飞书 / Lark | 真实任务系统 + 日程 + 通知 | 最适合做企业版 Stateboard adapter |
| 钉钉 / DingTalk | 企业待办 + 日程 + 群机器人 | 可接，但更依赖组织应用、用户身份和详情页 |
| 企业微信 / WeCom | 通知 + 日程 | 不建议单独作为主任务数据库 |

## 飞书推荐路径

```text
Codex automation
-> custom Feishu MCP / HTTP worker
-> Feishu Tasklist + Tasks + Reminders
-> Feishu bot card daily digest
```

适合原因：

- 任务可以成为飞书原生任务。
- 提醒和子任务能表达下一步动作。
- 机器人卡片适合推送每日摘要。
- 通过稳定 ID 映射可以做幂等更新。

需要：

- 飞书开放平台应用
- OAuth 或 tenant/user access token
- 任务、日历、消息权限
- 用户 ID 映射

## 钉钉推荐路径

```text
Codex automation
-> custom DingTalk worker
-> DingTalk work todo
-> DingTalk custom robot digest
```

限制：

- 更适合企业工作待办，不是轻量个人项目面板。
- 常需要 `detailUrl` 指回详情页。
- 用户身份、组织应用和权限配置更重。

## 企业微信推荐路径

```text
Codex automation
-> durable source of truth: Dida / Feishu / Notion
-> WeCom group robot or app message digest
-> optional WeCom calendar review event
```

判断：

- 企业微信适合触达和日程提醒。
- 群机器人是低成本摘要通道。
- 主任务状态建议仍放在滴答清单、飞书或 Notion。

## Skill 内部参考

更详细的来源和链接保留在：

```text
skills/stateboard-codex/references/integration-support.md
skills/stateboard-codex/references/todo-app-capability-matrix.md
```
