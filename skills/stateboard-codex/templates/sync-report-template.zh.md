# Sync Report Template

[English](sync-report-template.md)

每次运行结束后使用这份最终报告模板。发送前按用户请求语言调整 label。

```text
已同步到：{target_app} / {list_name}

本次更新：
- 更新任务：{updated_count}
- 新增任务：{created_count}
- 跳过/无新证据：{unchanged_count}

优先级变化：
- 升级：
- 降级：
- 保持：

验证：
- 写入结果：
- 搜索/读取验证：
- 自动化状态：

自动化：
- 名称：
- 频率：
- 下次运行：
- 如果本轮未创建自动化：写“未创建，待用户确认频率和具体时间”，不要编造 schedule。

问题：
- 连接器限制：
- 需要用户确认：
```

保持简短。除非用户要求，否则不要粘贴完整任务正文。
