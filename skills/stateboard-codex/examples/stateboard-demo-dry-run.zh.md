# Stateboard Demo Dry-run 示例

[English](stateboard-demo-dry-run.md)

这是 dry-run 示例，用来验证 `stateboard-codex` 在没有外部 connector 或不允许写入时，仍能产出可检查的项目状态任务。

## 输入

```text
我想整理的内容：当前 Stateboard 仓库
同步到：只输出 Markdown
目标位置：直接发给我
自动更新：不需要
```

## 预期输出

```text
标题：
P1｜Stateboard：AI 工作上下文项目状态板

项目定位：
把 Codex / ChatGPT / Agent 工作上下文整理成持续更新的项目状态板，并同步到待办、日程和团队协作工具。

当前进展：
项目定义、prompt 入口、skill 入口、集成模型和公开测试清单已沉淀。V1 保留 prompt quickstart 与 Codex skill 两种形态。

优先级：
P1。当前重点是验证 prompt 与 skill 两种入口都能生成项目状态任务，并能在目标系统中搜索和更新同一任务。

风险/边界：
- 不把 Stateboard 简化成普通 todo assistant。
- 不把 webhook 通知描述成完整任务系统。
- 不在用户未确认频率和具体时间时创建 automation。
- 不把历史上下文拆成大量低价值任务。

下一步建议：
- 继续维护 prompt 与 skill 的测试说明。
- 用带占位符的 task id mapping 模板记录幂等更新方式。
- 后续确认 automation 时间后再测试 recurring sync。

证据：
- docs/product-definition.md
- docs/prompt-template.md
- docs/testing.md
- skills/stateboard-codex/SKILL.md
```

## 验收

- 输出只有一个项目状态任务。
- 有明确证据来源。
- 没有外部写入。
- 没有 token、webhook、license key、私有 task id 或 project id。
