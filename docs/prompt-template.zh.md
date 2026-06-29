# Stateboard Prompt 模板

[English](prompt-template.md)

本文档是 prompt 入口索引，避免在多个位置维护重复模板。

正式可复制模板：

- `prompts/stateboard-sync-prompt.zh.md`：中文普通用户入口，只需要填写一次；手动同步和自动更新意图都在这一段里说明。
- `prompts/stateboard-sync-prompt.md`：英文主版。

高级模板：

- `prompts/stateboard-automation-prompt.zh.md`：供 agent 在用户已经确认自动更新时间后生成 Codex automation 使用，普通用户不需要直接填写。
- `prompts/stateboard-automation-prompt.md`：英文主版。

## 使用建议

- 想零安装快速验证：复制 `prompts/stateboard-sync-prompt.zh.md`。
- 想长期稳定复用：安装并使用 `skills/stateboard-codex/`。
- 想创建 recurring automation：仍然先复制 `prompts/stateboard-sync-prompt.zh.md`，在“自动更新”里写清楚频率和时间。

## 最小测试输入

```text
我想整理的内容：
当前 Stateboard 项目，或 `<你的项目路径>` 这个项目

同步到：
滴答清单

目标位置：
请新建一个叫“项目状态测试”的清单

自动更新：
不需要
```

## 不可省略的约束

- 先建立事实层，再判断项目状态。
- 只整理当前模型能读取或用户已经提供的内容。
- 写入前先搜索，优先更新同一任务。
- 不把历史记忆拆成大量低价值任务。
- 没有确认频率和具体时间时，不创建 automation；当前环境不支持自动化时，不假装已创建。
- 不写入 token、webhook、license key、私有凭据或私有目标系统标识。
- 默认用用户请求语言回复并写入目标系统；只有用户明确要求时才输出双语。
