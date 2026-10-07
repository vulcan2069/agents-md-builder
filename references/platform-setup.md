# 平台保存与启用指南

## 目标

访谈结束后，将规则交付到用户实际使用的平台。平台特性会更新：回答用户时先使用官方文档核对最新路径和加载方式；本文件提供保守默认值及官方入口，不代表所有版本/客户端都相同。

先确认三件事（访谈已覆盖就不再问）：

1. 用户使用的具体平台/客户端；可多选。
2. 生效范围：当前项目还是所有项目。
3. 当前 Agent 是否有目标工作区的写入权限，以及用户希望直接保存还是只拿内容。

## 通用交付逻辑

1. 若平台原生读取 `AGENTS.md` 且任务是项目级规则，保存为项目根目录 `AGENTS.md`。
2. 若平台用其他格式，优先生成一份平台原生文件。只有用户需要共享或维护统一规则时，才同时保留 `AGENTS.md` 主文件和适配文件；支持导入时使用原生导入语法，避免无意义复制两份全文。
3. 平台全局规则通常用于个人沟通偏好；项目文件通常用于项目协作规则。按用户选定范围保存，不要把项目细节塞进所有项目都加载的全局记忆。
4. 能写入时，检查目标文件是否已存在。已有文件先展示差异并询问合并或替换，不覆盖已有内容。
5. 不能写入时，输出可复制全文、准确目标路径、打开设置/导入的步骤，以及如何检查规则已加载。清楚说明用户需要手动完成哪一步。
6. 保存后尽可能重新读取文件核对内容。告诉用户若平台需重开会话/重载规则，应执行该步骤；有官方验证命令时给出命令。
7. 用户使用未列平台时，不猜路径。查看该平台官方文档；仍不能确认时，提供通用 Markdown 和手动添加到平台规则/项目上下文的保守步骤，并标注待验证。

## 常见平台

| 平台 | 项目级交付建议 | 全局/个人偏好 | 生效确认 |
|---|---|---|---|
| **Codex** | 项目根目录 `AGENTS.md`。如果平台可访问当前项目，访谈确认后可直接写入。 | `~/.codex/AGENTS.md` 可放跨项目指令；保存前确认用户确实要全局生效。 | 在 Codex 里询问它当前读取的指令文件，或查看对应工作区的文件。官方说明：[AGENTS.md 配置](https://developers.openai.com/codex/guides/agents-md)。 |
| **Claude Code** | 当前版本直接支持 `AGENTS.md`；只有 `CLAUDE.md`、配置或版本条件改变加载行为时，才提供 `CLAUDE.md` 适配（内容可用 `@AGENTS.md` 导入）。不要盲目同时创建两份不同正文。 | `~/.claude/CLAUDE.md` 是个人全局指令。 | 新会话中运行 `/memory` 或 `/context` 检查加载文件；AGENTS 支持与版本/Project instructions 设置有关。官方说明：[Project memory](https://code.claude.com/docs/en/memory)。 |
| **WorkBuddy** | 如果用户正在 WorkBuddy 的本地项目/文件任务中且授权目录可写，可以将 Markdown 保存到项目根目录；不要声称普通 WorkBuddy 对话一定会自动加载 `AGENTS.md`。 | 只有用户客户端提供明确的个人指令/记忆入口时才提示放入那里；不确定时提供手动粘贴说明。 | 区分“安装 Builder Skill”与“生成规则生效”。WorkBuddy 支持导入本地 Skill 包，但这本身不证明它会自动加载项目 `AGENTS.md`。官方说明：[WorkBuddy Skills](https://www.workbuddy.cn/docs/workbuddy/From-Beginner-to-Expert-Guide/Function-Description/Skills-Market)。 |
| **Cursor** | Cursor CLI 官方说明会读取项目根目录 `AGENTS.md`；IDE Agent 规则可生成 `.cursor/rules/<名称>.mdc`。用户同时使用 IDE 和 CLI 时建议保留主文件并按需提供规则适配。 | Cursor Settings → Rules 中的 User Rules，用于跨项目个人偏好。 | 检查 `.cursor/rules` 状态或在 Cursor CLI 会话中确认规则加载。官方说明：[Rules](https://docs.cursor.com/context/rules)、[Cursor CLI](https://docs.cursor.com/en/cli/using)。 |
| **GitHub Copilot** | 可使用项目根目录 `AGENTS.md`；仓库通用指令也可放 `.github/copilot-instructions.md`。按用户的 Copilot 使用表面选择，不能把 CLI 的行为无条件推及所有客户端。 | Copilot CLI 支持 `$HOME/.copilot/copilot-instructions.md`。其他界面使用各自的个人指令入口。 | Copilot CLI 用 `/instructions` 查看本次会话发现的指令。官方说明：[Copilot CLI instructions](https://docs.github.com/en/copilot/how-tos/copilot-cli/customize-copilot/add-custom-instructions)。 |
| **Gemini CLI** | 默认文件名为项目目录 `GEMINI.md`；用户可在设置中把 `AGENTS.md` 加入/设为上下文文件名。默认方案建议写 `GEMINI.md`，若多工具共用再确认是否使用统一命名配置。 | `~/.gemini/GEMINI.md` 是全局上下文。 | 运行 `/memory show` 检查合并后的上下文；更新后按需 `/memory refresh`。官方说明：[GEMINI.md](https://google-gemini.github.io/gemini-cli/docs/cli/gemini-md.html)。 |
| **CodeBuddy IDE（腾讯代码助手）** | 项目规则放 `.codebuddy/rules/`，内容按其规则文件格式保存；这与 WorkBuddy 桌面工作台是不同产品表面，不要混称。 | 用户级规则放用户目录下 `.codebuddy/rules/` 或在设置页建立。 | 新会话中检查规则；官方说明：[自定义规则](https://cloud.tencent.cn/document/product/1831/137462)。 |
| **Windsurf** | Windsurf 使用自己的 Rules/Memories 机制。官方文档若无法访问或已迁移，先查当前官方文档；无法确认时只交付 Markdown 并说明通过 Rules 设置添加，不猜文件路径。 | 在 Windsurf 的全局规则设置里保存个人偏好，按当前版本官方指引操作。 | 让用户从 Cascade/Rules 设置确认规则已启用；不依据第三方教程断言当前路径。官方入口：[Memories and Rules](https://docs.windsurf.com/windsurf/cascade/memories)。 |

## 其他聊天型 Agent

如果平台没有项目工作区、读取本地文件或持久规则入口：提供完整 Markdown，说明这是“可复制保存的文件内容”，并给出下载文件（仅当当前工具能实际生成文件时）。不要称为“已写入记忆”。可将项目级规则存为 `AGENTS.md`，再由用户上传、添加到项目上下文或粘贴到平台自定义指令中。

## 给用户的最终设置摘要

最后用简短步骤回答：

- **文件/规则名称与位置：** 实际路径或设置页面。
- **是否已保存：** 已保存并核对，或需要用户复制/导入。
- **启用步骤：** 例如重开会话、刷新规则、运行平台提供的查看命令。
- **生效范围：** 当前项目或所有项目。

不要把平台的“自动记忆”当成 `AGENTS.md` 的替代物；记忆是平台私有能力，项目规则是用户可管理和迁移的文件。
