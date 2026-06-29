# Stateboard 自动化 Prompt

[English](stateboard-automation-prompt.md)

这是高级模板，供 agent 在用户已经通过 `stateboard-sync-prompt.md` 确认频率和具体运行时间后，创建或更新 Codex automation。普通用户不需要直接填写这份 prompt。

```text
按已确认的频率和时间运行 Stateboard 同步。

运行计划：
【每日/每周 + 具体时间，例如 每周一 09:00】

整理范围：
【固定读取范围，例如指定 repo、项目说明、已有任务导出或用户选择的上下文文件】

目标系统：
【目标系统和目标清单/项目/数据库】

已有映射：
【已有目标任务 ID 映射；如果没有，先搜索稳定标题，再创建】

颗粒度：
【紧凑总览 / 平衡项目任务 / 详细行动清单】

规则：
- 先读取事实层，再判断项目状态。
- 更新已有任务优先，不重复创建。
- 只为真实活跃项目创建 durable project task。
- dormant 或低证据项目进入 parking lot。
- 不写入 secrets、token、webhook URL、webhook secret、license key、私有凭据或私有目标系统标识。
- 如果目标 connector 不可用，输出 Markdown fallback，并在报告中标记 blocked，不调用私有 API。
- 默认用用户请求语言回复，并用同一语言写入目标系统；只有用户明确要求时才输出双语。
- 输出短 run report，记录创建、更新、跳过、验证、阻塞。

如果运行计划、整理范围、目标系统或已有映射缺失，先询问，不要创建 automation。
```
