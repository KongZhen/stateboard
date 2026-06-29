# Integration Support

[中文](integration-support.zh.md)

This reference separates destination roles. It does not claim that every platform is writable in every runtime. Always discover available connectors before writing.

## Support Levels

| Level | Meaning |
|---|---|
| Direct connector | The current runtime exposes a tool that can create, search, and update destination items. |
| Official API | The platform has an official API or open platform, but the user must configure credentials, permissions, or a custom connector. |
| Notification / calendar | The platform is useful for digests or review blocks, but should not be treated as the primary task database. |
| Export fallback | No write connector is available; output Markdown, CSV-like rows, or copy/import instructions. |

## Common Destinations

| Destination | Recommended Stateboard role |
|---|---|
| Dida / TickTick / 滴答清单 | Primary personal task board when an MCP or official connector is available. |
| Notion | Project dashboard or documentation surface. |
| Google Calendar / Apple Calendar / Outlook Calendar | Review blocks and reminders, not the main task database. |
| Feishu / Lark / 飞书 | Strong enterprise task-system adapter candidate when an open-platform app is configured. |
| DingTalk / 钉钉 | Enterprise work todos and group digests; depends on organization app setup. |
| WeCom / 企业微信 | Notification and calendar layer; usually not the only project-task database. |
| Microsoft To Do / Apple Reminders | Good personal task destinations when an authorized connector or local automation path is available. |

## Required Runtime Behavior

Before writing:

1. Identify the requested destination.
2. Discover currently available tools/connectors.
3. If a connector exists, search existing destination tasks first.
4. If no connector exists, use export fallback and state that no external write happened.
5. Never call private or reverse-engineered APIs.

## Recommended Mapping

| Stateboard field | Task destination |
|---|---|
| project name + priority | stable task title |
| positioning, progress, blockers, evidence | task body |
| next actions | checklist / steps / subtasks |
| status review | calendar review block |
| summary digest | chat notification |

## Automation

Recurring sync requires an explicit user-confirmed schedule. Never invent a default time.
