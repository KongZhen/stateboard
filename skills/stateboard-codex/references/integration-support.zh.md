# 集成支持

[English](integration-support.md)

这份参考文档用于区分不同目标系统的角色。它不声称所有平台在所有运行环境里都能直接写入。写入前必须先发现当前可用 connector。

## 支持级别

| 级别 | 含义 |
|---|---|
| 直接 connector | 当前运行环境暴露了可创建、搜索、更新目标项目的工具。 |
| 官方 API | 平台有官方 API 或开放平台，但用户需要配置凭据、权限或自定义 connector。 |
| 通知 / 日程 | 平台适合摘要或复盘时间块，但不应被当作主任务数据库。 |
| 导出 fallback | 没有写入 connector；输出 Markdown、类 CSV 行或复制 / 导入说明。 |

## 常见目标系统

| 目标 | 推荐的 Stateboard 角色 |
|---|---|
| Dida / TickTick / 滴答清单 | 有 MCP 或官方 connector 时，适合作为个人主任务板。 |
| Notion | 项目 dashboard 或文档化状态页。 |
| Google Calendar / Apple Calendar / Outlook Calendar | 复盘时间块和提醒，不是主任务数据库。 |
| Feishu / Lark / 飞书 | 配好开放平台应用后，适合做企业任务系统 adapter。 |
| DingTalk / 钉钉 | 企业工作待办和群摘要；依赖组织应用配置。 |
| WeCom / 企业微信 | 通知和日程层；通常不作为唯一项目任务数据库。 |
| Microsoft To Do / Apple Reminders | 有授权 connector 或本地自动化路径时，适合作为个人任务目标。 |

## 必要运行行为

写入前：

1. 识别用户请求的目标系统。
2. 发现当前可用工具或 connector。
3. 如果 connector 存在，先搜索已有目标任务。
4. 如果没有 connector，使用导出 fallback，并说明没有发生外部写入。
5. 不调用私有或逆向 API。

## 推荐映射

| Stateboard 字段 | 任务目标系统 |
|---|---|
| 项目名 + 优先级 | 稳定任务标题 |
| 定位、进展、阻塞、证据 | 任务正文 |
| 下一步 | checklist / steps / subtasks |
| 状态复盘 | 日历复盘时间块 |
| 总结摘要 | 聊天通知 |

## 自动化

Recurring sync 必须使用用户明确确认的运行计划。不能编造默认时间。
