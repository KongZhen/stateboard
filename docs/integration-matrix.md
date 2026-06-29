# Integration Matrix

[中文](integration-matrix.zh.md)

This document records Stateboard's public integration model for todo, calendar, documentation, and collaboration destinations.

Key principle: never say "supports platform X" without naming the support tier.

## Support Tiers

```text
Tier 1: Direct connector available in the current runtime
Tier 2: Official API path exists, but requires app setup, permissions, tokens, or a custom connector
Tier 3: Notification / calendar layer, not a complete task database
Tier 4: Export / copy / Markdown fallback
```

## Common Destinations

| Target | Tier | Best use |
|---|---:|---|
| 滴答清单 / Dida / TickTick | Tier 1 or 2 | Primary personal task board when an MCP or official connector is configured |
| Google Calendar | Tier 1 or 2 | Project review blocks and reminders, not the task database |
| Notion | Tier 1 or 2 | Project dashboard or documentation surface |
| Codex Automations | Runtime feature | Scheduled refresh; not a destination task system |

## Enterprise Collaboration Platforms

| Platform | Recommended role | Judgment |
|---|---|---|
| 飞书 / Lark | Real task system + calendar + notification | Best candidate for enterprise Stateboard adapter |
| 钉钉 / DingTalk | Enterprise work todos + calendar + group robot | Viable, but depends more on organization apps, identity, and detail URLs |
| 企业微信 / WeCom | Notification + calendar | Not recommended as the only primary task database |

## Recommended Feishu/Lark Path

```text
Codex automation
-> custom Feishu/Lark MCP or HTTP worker
-> Feishu/Lark tasklist + tasks + reminders
-> Feishu/Lark bot card daily digest
```

Why this works:

- Tasks become native Feishu/Lark tasks.
- Reminders and subtasks can model next actions.
- Bot cards are good for daily digest delivery.
- Stable ID mapping makes idempotent updates possible.

Requires:

- Feishu/Lark open-platform app
- OAuth or tenant/user access token
- Task, calendar, and message permissions
- User ID mapping

## Recommended DingTalk Path

```text
Codex automation
-> custom DingTalk worker
-> DingTalk work todo
-> DingTalk custom robot digest
```

Limits:

- Better for enterprise work todos than lightweight personal project boards.
- Often requires `detailUrl` pointing to a backing detail page.
- User identity, organization app setup, and permissions are heavier.

## Recommended WeCom Path

```text
Codex automation
-> durable source of truth: Dida / Feishu / Notion
-> WeCom group robot or app message digest
-> optional WeCom calendar review event
```

Judgment:

- WeCom is strong for reach and calendar reminders.
- Group robots are a low-cost digest channel.
- Primary project-task state should usually live in Dida/TickTick, Feishu/Lark, or Notion.

## Skill References

More detailed sources and links live in:

```text
skills/stateboard-codex/references/integration-support.md
skills/stateboard-codex/references/todo-app-capability-matrix.md
```
