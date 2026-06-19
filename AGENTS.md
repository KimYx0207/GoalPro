## 项目语言

项目正文默认使用中文；保留必要专业术语，例如 Codex、Claude Code、Skill、Goal Contract、Token、README、Graphify。

## 项目目标

GoalPro 是一个 `goal` Skill 项目，用来把模糊需求压缩成可执行、可验证、低 Token 的 Goal Contract。

写作优先级：

1. 少废话，减少 Token。
2. 标准清楚：每个字段必须说明“写什么、合格标准、常见错误”。
3. 可执行：让 Codex / Claude Code 知道先读什么、做什么、何时停止、怎么证明完成。
4. 不把命令跑通当成用户目标完成。

## Graphify

本项目有 Graphify 知识图谱，输出在 `graphify-out/`。

规则：

- 代码或项目结构问题，若 `graphify-out/graph.json` 存在，先运行 `graphify query "<问题>"`。
- 查关系用 `graphify path "<A>" "<B>"`，查概念用 `graphify explain "<概念>"`。
- `graphify-out/` 是生成产物，不提交。
- 修改项目文件后，运行 `graphify update .` 更新本地知识图谱。
