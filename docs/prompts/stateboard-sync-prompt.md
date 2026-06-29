# Stateboard Sync Prompt

[中文](stateboard-sync-prompt.zh.md)

This is the zero-install Stateboard entry point. Copy the prompt below and replace the content inside brackets.

```text
Please organize the following projects or conversation context into a project-status board, then sync it to the destination I specify.

What I want to organize:
[For example: the last 60 days of Codex / ChatGPT / Claude / DeepSeek / WorkBuddy conversations that I can provide or you can read; the current project; a project folder; my existing todos; several pasted project chats]

Sync to:
[For example: Dida/TickTick, Notion, Google Calendar, Feishu/Lark, DingTalk, WeCom, or Markdown only]

Target location:
[For example: the "Project Control" list in Dida/TickTick; a Notion page/database; "create a new list called XXX"; if Markdown only, write "reply directly here"]

Automatic refresh:
[Not needed / daily HH:MM / weekly weekday HH:MM. If there is no clear time, write "not needed"]

Rules:
- Only use content you can read, search, or that I have provided. If some conversations or project materials are unavailable, tell me what is missing.
- Judge project state from evidence first. Do not split chat history directly into many tasks.
- By default, create or update only one project-status task per real project. Include current progress, risks/blockers, next steps, and evidence.
- Keep only 3-5 useful next steps per task.
- Search for existing tasks before writing. If a status task for the same project already exists, update it instead of creating a duplicate.
- If the target tool cannot be written to from the current environment, output a copy-ready Markdown version and explain the blocker.
- If I ask for automatic refresh but did not provide both frequency and exact time, ask me first. Do not assume any default time. If the current environment cannot create automation, give me copy-ready setup instructions instead of claiming it was created.
- Do not write tokens, webhook secrets, license keys, private credentials, or private destination identifiers.
- Respond and write destination content in the language of my request unless I explicitly ask for bilingual output.
- When done, tell me what was created, what was updated, how it was verified, and what still needs my confirmation.
```

## Minimum Test Input

```text
What I want to organize:
The current Stateboard project, or the project at <your-project-path>

Sync to:
Dida/TickTick

Target location:
Create a new list called Project Status Test

Automatic refresh:
Not needed
```
