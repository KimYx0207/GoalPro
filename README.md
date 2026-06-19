# GoalPro

GoalPro 是一个给 Codex 和 Claude Code 共用的 `goal` Skill 项目。

它的核心作用是：把模糊、宏大、容易跑偏的需求，整理成可执行、可验收、适合编码智能体执行的 Goal Contract。

说人话就是：先把“我要什么、做到什么算完、哪些不能做、怎么验证”讲清楚，再让智能体动手，减少瞎做、过度规划、假装完成。

本项目的质量重点不是把提示词写长，而是把 Token 用在标准上：

- 能删的说明删掉。
- 能合并的字段合并。
- 每个字段必须有明确合格标准。
- 不用流程包装弥补目标不清。

## 项目现在包含什么

```text
AGENTS.md                         Codex 项目说明
CLAUDE.md                         Claude Code 项目说明
.agents/skills/goal/              Codex 使用的 goal Skill
.claude/skills/goal/              Claude Code 使用的 goal Skill
.codex/hooks.json                 Codex 本地 hook 配置
.claude/settings.json             Claude Code 本地 hook 配置
```

其中最重要的是两份 Skill：

- `.agents/skills/goal/SKILL.md`
- `.claude/skills/goal/SKILL.md`

它们内容保持一致，分别服务 Codex 和 Claude Code。

## 这个 Skill 什么时候用

当用户提出这些需求时使用：

- 写一个高质量 goal / prompt
- 把模糊需求变成可执行任务
- 明确意图、范围、验收标准
- 给 Codex 准备 `/goal`
- 给 Claude Code 准备执行提示词
- 修复之前智能体输出跑偏、太复杂、假完成的问题

## Goal Contract 输出字段和标准

Skill 默认按这个顺序整理任务：

```markdown
Goal:
Outcome:
User value:
Scope:
Non-goals:
Context to read first:
Constraints:
Execution policy:
Checkpoints:
Verification:
Stop conditions:
Final report:
```

核心字段标准：

- `Goal`：一句话说清任务对象和动作；不写愿景口号。
- `Outcome`：写可观察结果；不能只写“完成优化”。
- `Scope`：列本次做什么；避免把未来计划塞进来。
- `Non-goals`：明确不做什么；用来防止过度发挥。
- `Context to read first`：只写会改变执行判断的文件、日志、截图、文档。
- `Constraints`：写硬限制，例如不删除、不发布、不改接口、不泄露密钥。
- `Execution policy`：写什么时候直接做、什么时候必须问。
- `Verification`：写证据类型，例如测试、diff、截图、线上状态、人工验收。
- `Stop conditions`：写必须暂停的风险点。

## 哪些文件不算项目核心

这些通常是本机运行产物或工具缓存，已经放进 `.gitignore`：

- `graphify-out/`：Graphify 生成的知识图谱输出
- `.meta-kim/`：Meta_Kim 当前运行状态、缓存、临时记录
- `.codex/`：Codex 本机 hook、绝对路径配置和排障脚本
- Python / Node 的缓存、虚拟环境、构建输出
- `.env`、编辑器配置、系统临时文件

注意：忽略不是删除。文件还在本机，只是以后不应该当成项目源码提交。

## 维护原则

- 优先改 `SKILL.md` 的触发说明和核心流程。
- 细节、来源、例子放到 `references/`，不要把 `SKILL.md` 写得过长。
- 如果改了 Codex 版本，也要同步 Claude Code 版本。
- 不要因为“看起来完整”就增加复杂机制；只有能防止真实失败时才加规则。
- 最终完成不能只看命令是否跑通，还要看用户目标是否真的达成。

## 当前状态

这个项目目前不是普通应用项目，没有 `package.json`、启动命令或测试框架。

它现在更像一个可复用 Skill 包：核心交付物是 `goal` Skill 本身，以及让 Codex / Claude Code 能正确识别和使用它的项目说明。
