# 测试

[English](testing.md)

修改 prompt、skill 或集成文档后，发布前按这份清单检查。

## Prompt

1. 把 `prompts/stateboard-sync-prompt.zh.md` 复制到 AI 助手里。
2. 填写四个面向用户的字段：
   - 想整理的内容
   - 同步到哪里
   - 目标位置
   - 是否自动更新
3. 先跑一次只输出 Markdown 的 dry-run。
4. 确认输出包含：
   - 每个真实活跃项目一条项目状态任务
   - 每条任务 3-5 个有用下一步
   - 当前进展、阻塞、优先级和证据
   - 清晰的运行报告

## Skill

1. 安装 skill：

   ```bash
   cp -R skills/stateboard-codex ~/.codex/skills/stateboard-codex
   ```

2. 新开一个 Codex 线程并运行：

   ```text
   $stateboard-codex

   我想整理的内容：当前项目
   同步到：只输出 Markdown
   目标位置：直接发给我
   自动更新：不需要
   ```

3. 确认 skill 与 prompt 遵循同一套行为规则。

## 可选真实同步

只有当用户已经选择目标系统并确认允许写入时，才执行真实同步。

第一次测试请使用单独的测试清单或页面，不要直接写入私人生产清单。

检查：

- 创建新任务前先搜索已有任务
- 第二次运行会更新同一条任务，而不是重复创建
- 任务正文和公开文件中没有 token、webhook secret、license key、凭据或私有目标系统标识
- 未确认频率和具体时间前，不创建 recurring automation

## 自动化门槛

只有在用户提供以下信息后，才能创建 automation：

- 整理范围
- 目标系统和目标位置
- 频率
- 具体运行时间
- 来源语言混合时的输出语言偏好

任何一项缺失，都要先询问，不能创建或更新 automation。
