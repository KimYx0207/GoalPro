---
name: goal
description: 把模糊、宏大或多步骤需求压缩成可执行、低 Token、可验证的 Goal Contract。用户要求写 goal、优化提示词、明确 done/success criteria、澄清意图、准备 Codex /goal、准备 Claude Code 执行任务、修复跑偏计划时使用。
---

# Goal Contract

目标：用最少必要 Token 写出能执行、能验收、少跑偏的 Goal Contract。

不要写长说明。把 Token 花在四件事上：意图、边界、标准、验证。

## 先判模式

- `Intake`：用户只要更好的 goal / prompt / spec。
- `Execution`：用户要 agent 按 goal 开始做。
- `Repair`：之前输出跑偏、太复杂、问太多、假完成。
- `Governed`：高风险、多文件、发布、外部事实、生产相邻任务。

用能诚实验收的最轻模式。

## 工作顺序

1. 提取真实意图：表面请求、真实结果、用户价值、最大跑偏风险。
2. 只 Fetch 会改变 goal 的材料：项目说明、点名文件、错误、截图、旧计划、当前外部事实。
3. 选结构：小任务单线；长任务加 checkpoints；互不冲突才并行。
4. 写 Goal Contract：短句、硬标准、可验证。
5. 自查：删掉空话，补齐验收，禁止把命令成功当完成。

## 字段标准

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

| 字段 | 写什么 | 合格标准 | 常见错误 |
|---|---|---|---|
| `Goal` | 一句话任务 | 有对象、有动作 | 写成愿景 |
| `Outcome` | 最终可见结果 | 能被观察或验收 | “优化完成” |
| `User value` | 为什么值得做 | 连接用户收益 | 空泛价值观 |
| `Scope` | 本次包含什么 | 只列本轮工作 | 塞未来计划 |
| `Non-goals` | 本次不做什么 | 防止越界 | 写“无”但任务很宽 |
| `Context to read first` | 先读材料 | 只列会影响判断的材料 | 全仓库漫游 |
| `Constraints` | 硬限制 | 权限、安全、兼容、语言 | 写成建议 |
| `Execution policy` | 直接做/先问规则 | 分清可逆与高风险 | 仪式化提问 |
| `Checkpoints` | 推进节点 | 每点有可检查输出 | 过程流水账 |
| `Verification` | 完成证据 | 测试、diff、截图、线上状态、人工验收分清 | 命令通过=完成 |
| `Stop conditions` | 必须暂停条件 | 路线、权限、删除、发布、密钥等风险 | 风险出现还继续 |
| `Final report` | 最后汇报 | 改了什么、证据、风险 | 大段复述过程 |

字段未知但不影响路线时，写默认假设。会改变路线、权限、风险、范围或验收时，先问。

## 输出规则

- 少写解释，多写标准。
- 小任务输出 6-8 个关键字段即可；复杂任务才用完整字段。
- Codex 执行场景给 `/goal` block。
- Claude Code 执行场景给任务提示词。
- Repair 场景先指出旧目标错在哪里，再给修正版。

## 验收清单

- 意图：说的是用户真正要的结果，不只是表面动作。
- 边界：保留用户限制，明确不做什么。
- Token：没有装饰性流程、套话、重复解释。
- 标准：每个关键字段能判断合格/不合格。
- 工具：只要求读取会改变判断的上下文。
- 证据：区分未验证、结构检查、本地验证、线上验证、人工验收。

## 需要更多细节时

- 方法依据：读 `references/source-rules.md`。
- 示例校准：读 `references/examples.md`。

## 最小输出形状

纯 goal 写作：

1. `Goal Contract`
2. `为什么这样写`
3. `阻塞问题`，仅在必须问时出现

执行准备：

1. `Codex /goal block` 或 `Claude Code 任务提示词`
2. `验证清单`
3. `暂停条件`

修复跑偏：

1. `旧目标的问题`
2. `修正后的 Goal Contract`
3. `防跑偏检查`
