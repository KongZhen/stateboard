# Task ID Mapping Template

[中文](task-id-mapping-template.zh.md)

Use this to record stable destination-task mappings. Do not commit mappings that contain private user IDs. Public examples must use placeholders.

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

Recommendations:

- Automation prompts may include private mappings, but open-source docs must only show placeholder formats.
- If no mapping exists, search stable titles before deciding whether to create or update.
- If priority changes, update the same task title in place instead of creating a new task.
