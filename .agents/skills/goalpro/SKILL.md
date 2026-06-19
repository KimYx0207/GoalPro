---
name: goalpro
description: 当用户要把模糊、战略性、多步骤、证据不足或容易跑偏的请求，整理成可执行、可验证、可暂停的 Goal Contract 时使用。适用于写 goal、优化任务提示词、明确 done/success criteria、deep research 后定战略、大改前 inventory、修复跑偏计划、为 Codex 或 Claude Code 准备执行任务。
---

# Goal Contract

目标：先把真实意图、战略判断、证据标准和成败边界讲清楚，再写成 Codex / Claude Code 能执行、能验收、少跑偏的 Goal Contract。

这不是“让提示词更短”的 Skill。表达经济只在战略完整后处理：删空话，不删判断、边界、证据和验收。

## 先判任务级别

- `Intake`：用户只要更好的 goal / prompt / spec。
- `Strategic`：用户要战略、方案、路线、标准、重要决策或高质量研究结论。
- `Execution`：用户要 agent 按 goal 开始做。
- `Repair`：之前输出跑偏、太粗糙、太复杂、问太多、假完成。
- `Governed`：高风险、多文件、发布、外部事实、生产相邻或会影响真实用户的任务。

用能诚实验收的最轻模式；但战略性任务必须先过证据门槛。

## Deep Research 门槛

出现任一条件，不得直接给最终战略 Goal，必须先 Fetch：

- 用户要求 `deep research`、`critical and fetch thinking and review`、全网搜索、行业/竞品/方法论研究。
- 任务依赖当前外部事实、最佳实践、规范、产品能力、法律/价格/版本/公开资料。
- 输出会决定路线、投入、架构、发布、长期标准或用户对“什么是好”的判断。
- 现有上下文不足以判断成败标准，且猜错会让执行明显跑偏。

Deep Research 执行顺序：

1. 定义研究问题：写清这次研究要改变哪个 Goal 判断。
2. 拆子问题：事实、规范、实践、失败、反证、决策影响，选 3-7 个。
3. 分来源层级：official / local / github / paper / reddit / x，不同来源权重不同。
4. 检索取证：每个关键子问题至少找 2 类来源；当前能力优先官方，本地落地优先项目文件，实践模式优先 GitHub，失败模式看 issue / Reddit，X 只作趋势信号。
5. 填 Evidence Map：每条证据都必须说明 claim、relevance、confidence、counterevidence、decision impact。
6. 反证检查：主动找能推翻当前路线的证据；冲突保留，不强行合并。
7. 定信心等级：high / medium / low，并说明依据。
8. 选输出形态：证据足够才输出 `Research-backed Goal Contract`；不足输出 `Draft Goal` 或 `Research Plan`。
9. 写回 Goal：研究结果必须改变 Decision standard、Evidence standard、Scope、Non-goals、Execution policy、Verification 或 Stop conditions；否则不算 deep research。

`Evidence Map` 格式：

```markdown
Evidence Map:
- Source:
  Source type:
  Claim:
  Relevance:
  Confidence:
  Counterevidence:
  Decision impact:
```

证据不足时，只能输出 `Draft Goal` 或 `Research Plan`，不能把草案说成最终战略。

## 工作顺序

1. Critical：先指出用户真正不满、要推进的局面、最大误伤点。
2. Fetch：只读取会改变战略、边界、验收或执行路线的材料；战略任务先做 deep research。
3. Thinking：比较路线，写清取舍；把反例、未知和信心等级放进判断。
4. Inventory：涉及代码库、文档库或复杂系统时，先列会受影响的文件、调用方、测试和验证入口，再允许执行。
5. Contract：写 Goal Contract，让执行者知道做什么、不做什么、先读什么、何时停。
6. Review：用成败标准反查合同，删掉装饰性流程，保留关键判断。
7. Expression economy：最后才压缩表达；不得牺牲意图完成度。

社区来源只能作为信号：GitHub 项目、X 经验帖、Reddit 讨论可以暴露失败模式和实践趋势，但必须被官方文档、本地证据或多来源重复信号支撑后，才进入最终 Goal。

## 战略标准

一个 Goal 达标，必须回答清楚：

- `真实意图`：用户真正要改变的局面，不是复述原话。
- `战略结果`：完成后什么会变好，为什么值得做。
- `成败标准`：什么算赢，什么算没做到，必须可判断。
- `证据标准`：需要哪些来源、验证或观察来支撑判断。
- `关键边界`：范围、权限、风险、语言、质量要求和不做事项。
- `取舍逻辑`：速度、范围、质量、表达成本冲突时保什么、舍什么。
- `反证与未知`：哪些证据会推翻当前路线，哪些问题必须暂停。
- `上下文策略`：哪些内容常驻，哪些按需读取，哪些写入可恢复的计划文件。

## 字段标准

```markdown
Goal:
Intent:
Strategic outcome:
Decision standard:
Evidence standard:
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

| 字段 | 写什么 | 合格标准 | 常见错误 |
|---|---|---|---|
| `Goal` | 一句话任务 | 有对象、有动作、有方向 | 写成愿景 |
| `Intent` | 放大后的真实意图 | 说清用户真正要改变的局面 | 复述原话 |
| `Strategic outcome` | 最终战略结果 | 能解释为什么这次工作值得做 | 只写交付物 |
| `Decision standard` | 路线判断标准 | 明确优先级、取舍和失败条件 | “高质量”但不可判 |
| `Evidence standard` | 证据要求 | 区分来源、验证、人工验收和信心等级 | 搜到资料就算完成 |
| `Scope` | 本次包含什么 | 只列本轮工作 | 塞未来计划 |
| `Non-goals` | 本次不做什么 | 防止越界 | 写“无”但任务很宽 |
| `Context to read first` | 先读材料 | 只列会改变判断的材料 | 全仓库漫游 |
| `Constraints` | 硬限制 | 权限、安全、兼容、语言 | 写成建议 |
| `Execution policy` | 直接做/先问规则 | 分清可逆与高风险 | 仪式化提问 |
| `Checkpoints` | 推进节点 | 每点有可检查输出 | 过程流水账 |
| `Verification` | 完成证据 | 测试、diff、截图、线上状态、人工验收分清 | 命令通过=完成 |
| `Stop conditions` | 必须暂停条件 | 路线、权限、删除、发布、密钥等风险 | 风险出现还继续 |
| `Final report` | 最后汇报 | 改了什么、证据、风险 | 大段复述过程 |

字段未知但不影响路线时，写默认假设。会改变路线、权限、风险、范围或验收时，先问。

## 输出位置规则

- 默认位置：聊天窗口。用户要求写 goal、优化提示词、准备 `/goal`、准备 Claude Code 任务时，直接在聊天窗口输出可复制的 fenced `markdown` 代码块。
- 文件位置：只有用户明确要求保存、写入文件、生成文档、提交 git、更新项目资料，才把 Goal Contract 写入文件。
- 双输出：一旦写入文件，聊天窗口仍必须同步输出同一份可复制的 goal 提示词代码块，并说明文件路径。
- 不确定时：默认聊天窗口输出，不要为了“完整”自动创建文件。
- 文件建议路径：目标文档优先用 `docs/goals/<topic>.md`；示例、方法依据或 Skill 本体改动仍放回对应 `references/` 或 `SKILL.md`。
- 代码块要求：可复制提示词必须放在 fenced `markdown` code block 内；不要只给文件链接或摘要。

## 输出模式

- 普通 goal：输出 `Goal Contract`、`为什么这样写`、必要时的 `阻塞问题`。
- 战略/研究 goal：输出 `Research-backed Goal Contract`、`Evidence Map 摘要`、`反证/未知`。
- Codex 执行场景：给 `/goal` block，包含 done-when、read-first、checkpoints、pause-if。
- Claude Code 执行场景：给任务提示词，包含先读材料、执行策略、验证和暂停条件。
- 大改/重构场景：先输出 inventory、影响面、分片计划、每片验证；不得先重构再补解释。
- Repair 场景：先指出旧目标哪里错，再给修正版和防跑偏检查。

## 验收清单

- 意图：说的是用户真正要的结果，不只是表面动作。
- 战略：说明结果价值、成败标准、证据标准和关键取舍。
- Deep Research：战略或外部事实任务有来源、反证、信心等级和决策影响。
- Community Signal：GitHub / X / Reddit 只当候选证据，已说明来源类型和采纳理由。
- Inventory：复杂代码任务先有影响面地图，再进入实现。
- 边界：保留用户限制，明确不做什么。
- 标准：每个关键字段能判断合格/不合格。
- 位置：默认聊天窗口给 fenced `markdown` 代码块；写文件时也要同步给代码块和文件路径。
- 工具：只要求读取会改变判断的上下文。
- 证据：区分未验证、结构检查、本地验证、线上验证、人工验收。
- 表达：压缩只删空话，不删意图、边界、标准和验证。

## 需要更多细节时

- 方法依据：读 `references/source-rules.md`。
- 示例校准：读 `references/examples.md`。
