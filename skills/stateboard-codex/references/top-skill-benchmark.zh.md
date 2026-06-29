# 顶级 Skill 评测基准

[English](top-skill-benchmark.md)

用这份 checklist 确保 skill 是强可复用 agent 能力，而不是一次性脚本。

## 1. 精准触发

好的 skill 必须触发范围明确。

这个 skill 应该在“项目上下文 -> todo dashboard”场景触发，而不是所有提醒请求。

## 2. 副作用前必须 intake

创建任何内容前，skill 必须确认：

- 目标 app / 清单
- 自动化时间 / 频率
- 来源范围
- 颗粒度

可以先创建草稿计划，但不能先创建 recurring automation。

## 3. Connector-aware 执行

skill 不应该默认 TickTick / Dida。

它应该：

- 发现可用 MCP 工具
- 优先使用官方 connector
- 优雅降级为可导入输出
- 明确说明能力限制

## 4. 幂等写入

顶级 skill 会避免重复任务污染。

要求：

- 创建前先搜索
- 更新已知任务 ID
- 在 automation prompt 或本地状态中保留映射
- 只为新的高信号项目创建任务

## 5. 证据质量

每个项目状态都应该有来源支撑：

- memory summary
- repo 文件
- 项目说明 / current state 文档
- 最近任务结果
- automation 运行结果

如果没有新证据，就明确说明。

## 6. 颗粒度控制

好的 skill 知道什么时候不要创建任务。

规则：

- 默认一个项目一条任务
- 不为历史记录建任务
- 休眠项目进入 parking lot
- 除非用户要求，否则每个项目最多 3-5 个下一步

## 7. 验证

写入后：

- 搜索 / fetch 关键任务
- 只有有意创建测试任务时，才验证测试任务完成状态
- 验证 automation 状态和 schedule
- 把搜索索引延迟和写入失败分开报告

## 8. 跨 app 可移植性

skill 应该保留语义模型：

```text
Project -> Status -> Priority -> Next actions -> Blockers -> Evidence
```

再映射到每个 app 可用的结构：

- TickTick / Dida：project/list + tasks + tags + priority + checklist
- Microsoft To Do：list + task + steps + reminders
- Apple Reminders：list + reminders + subtasks + tags/smart lists
- Calendar：review block，不是任务数据库
- 轻量 app：紧凑、可复制任务

## 9. 自动化安全

Recurring automation 应该：

- 使用用户确认过的 schedule
- 原地更新
- 避免 secret 泄漏
- 不修改项目代码
- 输出短 run report

## 10. 可安装打包

交付成完整目录：

```text
skill-name/
  SKILL.md
  references/
  templates/
```

保持根 `SKILL.md` 简洁，把市场 / app 细节放进 references。
