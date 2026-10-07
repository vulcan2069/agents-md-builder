# AGENTS.md Builder

## 这是什么？

一个通过对话帮你写出个人 Agent 合作说明书 `AGENTS.md` 的 Skill。

## 为什么需要它？

每次都重新解释沟通习惯、权限和完成标准很费力。`AGENTS.md` 可以把稳定偏好写下来，让 Agent 在项目中按同一套约定工作。

## 它怎么工作？

访谈 → 整理个人 Profile → 请你确认理解 → 转成可执行规则 → 检查并输出 `AGENTS.md`。访谈分几轮进行，不会直接套模板；不相关的问题会跳过。

## 示例

你说：“我不会编程，用 Codex 做 Python 小工具。简单任务直接做，删文件或安装依赖先问。请用简单中文解释，并运行脚本检查结果。”

可能形成的规则：“修改脚本后运行相关检查并说明结果；删除文件或安装依赖前先征求同意；使用专业术语时先解释。”

## 设计理念

这不是模板生成器，而是一个对话式的个人 Agent 协作约定构建器。只有能改变 Agent 实际行为的规则才值得写入。

## 文件说明

- `SKILL.md`：入口、访谈流程、确认门和生成要求。
- `references/interview-framework.md`：动态问题库、跳过条件和冲突处理。
- `references/agents-md-template.md`：章节结构及按用户类型组合的方法。
- `references/rule-writing-guide.md`：将自然语言转成可执行规则的写法。
- `references/rule-lint.md`：生成前逐条检查规则质量。
- `references/platform-setup.md`：按 Codex、Claude Code、WorkBuddy 等平台提供保存位置和启用验证步骤。
- `examples/`：四类用户的访谈路径与差异化结果。
