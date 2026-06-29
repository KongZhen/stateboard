# Sync Report Template

[中文](sync-report-template.zh.md)

Use this as the final report after each run. Translate labels to the user's request language before sending.

```text
Synced to: {target_app} / {list_name}

This run:
- Updated tasks: {updated_count}
- Created tasks: {created_count}
- Skipped / no new evidence: {unchanged_count}

Priority changes:
- Raised:
- Lowered:
- Unchanged:

Verification:
- Write result:
- Search/read verification:
- Automation status:

Automation:
- Name:
- Frequency:
- Next run:
- If no automation was created this run: write "Not created; awaiting confirmed frequency and exact time." Do not invent a schedule.

Issues:
- Connector limits:
- Needs user confirmation:
```

Keep it short. Do not paste full task bodies unless the user asks.
