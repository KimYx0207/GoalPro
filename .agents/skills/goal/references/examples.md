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
搜索全网，帮我写一个高质量 goal Skill，要支持 Codex 和 Claude Code，必须能分析真实意图并执行好。
```

合格输出必须先声明研究门槛：

```markdown
Research required:
这是战略型 Skill 设计任务，依赖当前 Codex / Claude Code / Agent Skills / deep research 最佳实践。没有 deep research 只能给草案，不能给最终战略。

Evidence Map 摘要:
- Codex goal 文档：goal 要写成完成契约，包含结果、约束和可验证 done-when。
- Claude / Agent Skills 文档：description 是触发表面，必须描述使用场景，不能塞次要优化目标。
- Deep Research / PRISMA / GRADE：战略判断要有来源范围、反证、信心等级和决策影响。
- GitHub / Reddit / X 社区信号：把 plan、inventory、diff、verify 做成短循环；社区信号只作候选，必须交叉验证。

Research-backed Goal Contract:
Goal:
重建 goal Skill，使它先放大真实意图和战略标准，再生成 Codex / Claude Code 可执行、可验证的 Goal Contract。

Intent:
解决 agent 接到模糊任务后跑偏、过度计划、假完成的问题；不是追求短提示词，而是追求战略判断正确。

Strategic outcome:
用户能把高风险、模糊、长期或研究型任务交给 agent 前，先得到一份能约束执行、验收和暂停条件的任务契约。

Decision standard:
意图完成度 > 证据质量 > 可执行性 > 表达经济。任何表达缩减都不能损害成败标准、边界、反证和验证。

Evidence standard:
战略任务必须先 fetch 权威来源和反证；普通项目任务必须先读会改变路线的本地材料；最终报告必须区分未验证、结构检查、本地验证、线上验证和人工验收。
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
用户能直接复制这段提示词使用；提示词包含目标、意图、标准、执行策略和验证。
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
使用 goal Skill，把下面请求整理成可执行任务；目标清楚后再实现。

先读 `CLAUDE.md` 和用户点名文件。若请求依赖外部事实、战略判断或高质量研究，先做 deep research 并给证据地图；若存在会改变范围、风险或验收的多条路线，先通过原生提问界面问我。

若请求涉及大改、重构或跨模块行为，先输出 inventory 和分片验证计划，不要直接修改代码。

请求：
[用户请求]
```
