# Task ID Mapping Template

[English](task-id-mapping-template.md)

用于记录目标系统里的稳定任务映射。不要把包含用户私有 ID 的映射提交到公开仓库；公开示例必须脱敏。

```text
target_app: Dida / TickTick
destination_name:
destination_id: <private, do not commit>

tasks:
  - stable_title:
    project_slug:
    priority:
    task_id: <private, do not commit>
    last_verified_at:
    verification_method: search | fetch | write_return
    notes:
```

建议：

- automation prompt 可以携带私有映射，但开源文档只写脱敏格式。
- 如果没有映射，先搜索 stable title，再决定创建或更新。
- priority 变化时更新同一任务标题，不创建新任务。
