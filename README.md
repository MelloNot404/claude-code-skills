# claude-code-skills

一组用于 Claude Code 的轻量级个人 Skill，专注于低风险小修改、任务交接和本地会话归档。

这不是完整 Agent 框架。它的默认假设是：Codex 负责复杂、高可靠性工作；Claude Code 可以在成本敏感或额度紧张时，作为简单任务的低成本执行层。

## 包含的 Skills

| Skill | 说明 |
|-------|------|
| [safe-edit](./safe-edit/SKILL.md) | Codex 的低成本备用助手，仅处理简单、低风险、范围清晰的小修改（通常 1~3 个文件）。 |
| [handoff-to-codex](./handoff-to-codex/SKILL.md) | 当任务变复杂时，生成简洁的交接记录供 Codex 接手，不自行继续排查。 |
| [end](./end/SKILL.md) | 结束当前会话，将本次对话总结归档到本地 `worklog\` 目录下的 txt 工作日志。 |

## 安装方式

1. 将对应 Skill 文件夹（如 `safe-edit/`）复制到 Claude Code 的个人 Skills 目录：

   ```
   %USERPROFILE%\.claude\skills\
   ```

2. 在 Claude Code 会话中通过 `/skill-name` 调用。

## 调用示例

```
/safe-edit 修改按钮文字并调整间距
/handoff-to-codex 用户注册功能未完成，请生成交接记录
/end
```

## 安全原则

- 不处理或输出 `.env`、API Key、token、密码、credential 等敏感内容
- 不自动执行 `git commit`、`git push`、`git reset --hard`
- 不默认安装任何依赖
- 不替代人工代码审查
- 不提交 `worklog/`、本地备份、个人配置或包含敏感上下文的归档文件

## 注意事项

- 这些 Skill 是轻量级工作流工具，不保证适合高风险或复杂工程任务
- 超出 safe-edit 范围的任务（架构重构、数据库迁移、安全认证等）应使用 Codex 或其他方式处理
- handoff-to-codex 仅生成记录，不继续排查问题
- **end 的归档路径**：默认归档到当前项目下的 `worklog\` 目录。用户可自行修改 SKILL.md 中的路径配置，指向自己的本地工作日志目录
- **归档文件属于本地工作记录**，可能包含项目上下文和待办事项，不应上传到公开仓库。请确保 `.gitignore` 已包含 `worklog/` 规则
