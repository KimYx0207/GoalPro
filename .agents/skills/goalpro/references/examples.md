# Goal Skill 示例

这个文件用于校准输出形状，不要在普通小任务里加载。

## 模糊开发请求

输入：

```text
做个登录功能
```

输出：

```markdown
Goal:
实现用户登录。

Intent:
让已有用户安全进入受保护区域，同时不破坏项目现有认证体系。

Strategic outcome:
项目获得一条可维护的基础认证路径，后续权限、账户和审计能力能复用它。

Decision standard:
优先复用现有认证模式；安全和兼容性高于从零设计；不在本轮扩展注册和 OAuth。

Evidence standard:
先读现有用户模型、认证路由、会话中间件和测试命令；用测试和一次手动登录证明行为。

Scope:
登录入口、凭据校验、会话或 token、错误处理、最小测试。

Non-goals:
注册、找回密码、OAuth、角色系统，除非项目已有且本次必须联动。

Context to read first:
项目说明、用户模型、认证路由、会话中间件、测试命令。

Constraints:
不明文存密码；不打印 token；复用现有认证结构。

Execution policy:
如果项目已有认证模式，直接沿用；如果必须在 session 和 token 之间选型且无现有模式，先问。

Verification:
正确账号可登录；错误账号失败；认证测试通过；可运行时手动验证一次。

Stop conditions:
找不到用户模型，或需要新增认证存储决策。

Final report:
改动文件、行为变化、验证结果、剩余风险。
```

## 战略研究请求

输入：

```text
搜索全网，帮我写一个高质量 goalpro Skill，要支持 Codex 和 Claude Code，必须能分析真实意图，并生成后续 Agent 能执行好的 goal。
```

合格输出必须先声明研究门槛：

```markdown
Research required:
这是战略型 Skill 设计任务，依赖当前 Codex / Claude Code / Agent Skills / deep research 最佳实践。没有 deep research 只能给草案，不能给最终战略。

Research question:
判断 goalpro Skill 应该如何同时满足 Codex / Claude Code 触发、战略意图放大、deep research、输出位置、prompt-only 停止和生成 goal 的可执行性要求。

Subquestions:
1. 官方文档如何定义 goal / skill 的触发、完成标准和可验证停止条件？
2. 高质量 GitHub 项目如何组织 skill、references、examples？
3. Reddit / issue 中真实用户在哪些场景里跑偏？
4. X / 社区实践有哪些短循环信号，需要哪些交叉验证？
5. 哪些证据会推翻“默认聊天输出、输出后停止、显式才写文件或执行”的路线？

Evidence Map 摘要:
- Source type: official
  Claim: Codex goal 要写成完成契约，包含结果、约束和可验证 done-when。
  Decision impact: 写入 `Decision standard` 和 `Verification`。
- Source type: official
  Claim: Claude / Agent Skills 的 `description` 是触发表面，必须描述使用场景，不能塞次要优化目标。
  Decision impact: 禁止把表达压缩写进 `description`。
- Source type: method
  Claim: Deep Research / PRISMA / GRADE 要说明来源范围、反证、信心等级和决策影响。
  Decision impact: 增加 `Evidence standard` 和 `Stop conditions`。
- Source type: github / reddit / x
  Claim: 社区高频实践是 plan、inventory、diff、verify 短循环；社区信号只能作候选，必须交叉验证。
  Decision impact: 增加 inventory、社区信号权重和反模式。

Counterevidence:
- 社区帖子可能只适用于作者自己的工具链。
- 过度流程会让小任务变慢。
- 如果用户只是要一个提示词，写文件会降低用户体验。

Confidence:
medium-high。官方文档和本地项目证据支持核心规则；社区信号只作为失败模式和实践趋势，不单独决定标准。

Research-backed Goal Contract:
Goal:
重建 goalpro Skill，使它先放大真实意图和战略标准，再生成 Codex / Claude Code 可执行、可验证、可暂停的 Goal Contract，并在没有执行授权时停止。

Intent:
解决 agent 接到模糊任务后跑偏、过度计划、假完成的问题；不是追求短提示词，而是追求战略判断正确。

Strategic outcome:
用户能把高风险、模糊、长期或研究型任务交给 agent 前，先得到一份能约束执行、验收和暂停条件的任务契约。

Decision standard:
意图完成度 > 可执行性 > 证据质量 > prompt-only 停止 > 表达经济。任何表达缩减都不能损害成败标准、边界、反证、验证和授权边界。

Evidence standard:
战略任务必须先 fetch 权威来源和反证；普通项目任务必须先读会改变路线的本地材料；最终报告必须区分未验证、结构检查、本地验证、线上验证和人工验收。

Execution policy:
默认只输出 fenced `markdown` Goal Contract；不要继续改文件、运行命令或提交。只有用户明确授权执行时，才把生成的 goal 交给后续 agent 执行。

Stop conditions:
来源互相冲突且影响核心规则；关键证据缺失；研究没有改变 Goal Contract 字段；用户没有授权执行但上下文开始要求继续做事。
```

## 大改或重构请求

输入：

```text
把订单模块重构一下，现在太乱了
```

输出必须先阻止“直接重构”：

```markdown
Goal:
重构订单模块中影响维护性的核心路径，并保持现有业务行为不变。

Intent:
用户真正要的是降低订单模块后续修改成本，不是追求大面积改写。

Strategic outcome:
订单模块的职责边界、调用关系和验证入口变清楚，后续改需求能更快定位影响面。

Decision standard:
行为兼容 > 可验证切片 > 结构清晰 > 改动范围。禁止无 inventory 的大面积移动文件。

Evidence standard:
先列 inventory：订单相关入口、调用方、数据库/接口边界、现有测试、手动验证路径。每个重构切片必须绑定一个最小验证。

Context to read first:
- 订单模块入口
- 调用订单模块的 API / service / UI
- 订单相关测试
- 构建和测试命令

Execution policy:
先输出 inventory 和分片计划；用户或当前任务允许后，再按最小切片改。每片后运行对应测试或说明无法验证。

Checkpoints:
1. Inventory：影响文件、调用方、测试入口。
2. Slice 1：无行为变化的命名/抽取，验证相关测试。
3. Slice 2：职责拆分或边界整理，验证订单主流程。
4. Final review：diff、行为风险、未覆盖路径。

Stop conditions:
找不到订单行为验收路径；需要改数据库语义；发现多个互斥架构路线；测试无法运行且无手动验证办法。
```

## 修复跑偏请求

输入：

```text
这个不对，太复杂了
```

输出必须做到：

- 指出被否定的是上一版目标或计划。
- 把“太复杂”当成范围失败，不要继续解释上一版为什么合理。
- 给更小的 Goal Contract。
- 明确删掉了哪些工作。
- 如果旧版把次级目标当核心目标，必须改回用户真实意图。

## 意图错位自检

输入：

```text
帮我优化一下这个项目
```

不合格输出：

```markdown
Goal:
优化项目，提高质量。

Intent:
用户想让项目更好。
```

合格输出必须补齐：

- 用户点名项目或当前工作区；如果没有目标对象，先问或写明默认假设。
- `Intent` 说明用户真正不满的是可维护性、体验、性能、文档、交付可信度，还是 Agent 已经跑偏。
- `Strategic outcome` 说明完成后局面怎么变，而不是只说“更好”。
- `Decision standard` 能区分该优先小修、重构、研究、清理还是只写 goal。
- `Context to read first` 只列会改变判断的材料。
- `Verification` 对应用户目标；不能只写“测试通过”。

## 聊天窗口直接输出

输入：

```text
用这套 skill，帮我做个目标，优化这个 skill
```

输出位置必须是聊天窗口，不创建文件：

````markdown
下面是可直接复制的 goal 提示词：

```markdown
Goal:
优化 GoalPro 的 `goal` Skill，使它更稳定地把模糊、战略性、多步骤或证据不足的请求转成可执行、可验证、可暂停的 Goal Contract。

Intent:
用户要的是一份能直接复制给 Codex 或 Claude Code 的目标提示词，不是项目文件。默认在聊天窗口输出，除非用户明确要求保存或提交。

Strategic outcome:
后续优化能围绕意图完成度、成败标准、证据标准、输出位置和验证规则推进，而不是凭感觉改文案。

Decision standard:
用户体验 > 意图完成度 > 成败可判 > 证据质量 > 执行约束 > 表达经济。

Execution policy:
只在聊天窗口输出 fenced `markdown` 代码块；不创建文件、不提交 git。

Verification:
用户能直接复制这段提示词使用；提示词包含目标、意图、标准、执行策略和验证；输出后停止，不继续优化文件本身。
```
````

## 文件加聊天双输出

输入：

```text
把这个目标保存到 docs/goals/optimize-goal-skill.md，也在聊天里给我一份可复制版本。
```

输出必须同时满足：

- 写入用户指定文件，或使用 `docs/goals/<topic>.md`。
- 聊天窗口同步输出同一份 fenced `markdown` 代码块。
- 最后说明文件路径。

````markdown
已写入：`docs/goals/optimize-goal-skill.md`

聊天窗口可复制版本：

```markdown
Goal:
[完整 Goal Contract 内容]

Intent:
[完整 Intent 内容]

Verification:
[完整 Verification 内容]
```
````

## Codex `/goal` 示例

```markdown
/goal
把项目从 JavaScript 迁移到 TypeScript。

Intent:
提升项目长期可维护性和类型安全，同时保持现有用户行为不变。

Strategic outcome:
项目拥有可持续演进的类型基础，后续功能开发能更早暴露接口和数据错误。

Decision standard:
行为兼容高于迁移速度；严格类型高于一次性大改；不为了减少改动而保留无意义 `any`。

Done when:
- 应用能在 strict mode 下编译。
- 不新增显式 `any`，除非有注释说明无法避免。
- 现有用户行为不变。
- 构建和现有测试通过。

Read first:
- AGENTS.md
- package scripts
- tsconfig 或构建配置
- 源码入口

Work in checkpoints:
1. 建立当前 build/test 基线。
2. 转换配置和入口。
3. 小批量转换模块。
4. 每批后运行 build/tests。

Pause if:
- 需要升级依赖。
- 自动重写会碰到无关行为。
- 验证无法运行。
```

## Claude Code 任务提示词示例

```markdown
使用 goalpro Skill，把下面请求整理成可执行任务；目标清楚后再实现。

先读 `CLAUDE.md` 和用户点名文件。若请求依赖外部事实、战略判断或高质量研究，先做 deep research 并给证据地图；若存在会改变范围、风险或验收的多条路线，先通过原生提问界面问我。

若请求涉及大改、重构或跨模块行为，先输出 inventory 和分片验证计划，不要直接修改代码。

请求：
[用户请求]
```
