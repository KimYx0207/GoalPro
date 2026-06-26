# Goal Skill 示例

这个文件用于校准输出形状，不要在普通小任务里加载。

## 模糊开发请求

输入：

```text
做个登录功能
```

输出：

Goal Prompt:

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

Loop Prompt:

```markdown
Loop mission:
持续推进“已有用户安全进入受保护区域”这个目标；每轮只关闭最影响登录闭环的差距，直到登录能力达到可验收状态。

Loop state:
继承原始登录目标、当前轮次、已关闭验证证据、开放风险、下一轮焦点和暂停原因；不要每轮重新定义登录范围。

Previous result to inspect:
上一轮最终报告、diff、认证相关测试输出、手动登录记录、错误日志、用户反馈。

Review evidence:
区分“测试通过”“手动登录成功”“安全边界已检查”和“只在报告中声称完成”。不要把没有证据的完成声明当成完成。

Gap diagnosis:
按安全阻塞、核心登录失败、受保护区域进入失败、错误处理不清、体验细节排序剩余差距。

Cycle action:
只修复本轮最高价值差距；不扩展注册、找回密码、OAuth 或角色系统，除非上一轮结果证明它们是当前登录闭环的阻塞。

Verification delta:
补齐上一轮缺失的最小验证，并说明本轮新增证据如何关闭剩余差距。

Loop guardrails:
最多连续 3 个 LOOP 周期；若连续 2 轮仍无法关闭登录阻塞、同一安全风险重复出现、验证不可运行，或需要认证选型/数据模型/安全策略判断，则 Pause。

Continuation protocol:
每轮结束判定 `Done`、`Continue` 或 `Pause`。若登录闭环仍有未关闭且可继续处理的差距，必须输出下一轮 `Next LOOP packet`；如果认证选型、数据模型或安全策略需要产品判断，暂停问用户。

Stop / escalate conditions:
需要新增认证存储、改密码策略、接入第三方身份服务、处理真实用户数据、发布上线或变更安全边界时暂停。

Next LOOP packet:
包含原始登录目标、当前轮次、已关闭证据、开放差距、下一轮焦点、要读取的材料、暂停条件和本轮新增验证。
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

Research-backed Goal Prompt:
Goal:
重建 goalpro Skill，使它先放大真实意图和战略标准，再生成 Codex / Claude Code 可执行、可验证、可暂停的 Goal Prompt，并附带交付后继续进化用的 Loop Prompt；没有执行授权时停止。

Intent:
解决 agent 接到模糊任务后跑偏、过度计划、假完成的问题；不是追求短提示词，而是追求战略判断正确。

Strategic outcome:
用户能把高风险、模糊、长期或研究型任务交给 agent 前，先得到一份能约束执行、验收和暂停条件的任务契约。

Decision standard:
意图完成度 > 可执行性 > 证据质量 > prompt-only 停止 > 表达经济。任何表达缩减都不能损害成败标准、边界、反证、验证和授权边界。

Evidence standard:
战略任务必须先 fetch 权威来源和反证；普通项目任务必须先读会改变路线的本地材料；最终报告必须区分未验证、结构检查、本地验证、线上验证和人工验收。

Execution policy:
默认只输出 fenced `markdown` Goal Prompt + Loop Prompt；不要继续改文件、运行命令或提交。只有用户明确授权执行时，才把生成的 goal 交给后续 agent 执行。

Stop conditions:
来源互相冲突且影响核心规则；关键证据缺失；研究没有改变 Goal / Loop 字段；用户没有授权执行但上下文开始要求继续做事。

Loop Prompt:
Loop mission:
持续推进 goalpro Skill，使它稳定地从模糊人类意图产出交付级 Goal Prompt，并附带可持续收敛的 Loop Prompt。

Loop state:
继承原始改造目标、当前轮次、已验证规则、未关闭差距、镜像状态、模糊意图自测结果和下一轮焦点。

Previous result to inspect:
最终报告、README diff、`.agents` 和 `.claude` skill diff、source-rules / examples diff、镜像一致性检查、模糊意图自测输出。

Review evidence:
区分文案声明、静态 diff、镜像一致性、prompt-only 边界验证、模糊意图实测和交付级产品可执行性证据。

Gap diagnosis:
优先找三类差距：是否仍只输出单一 Goal Contract；Loop 是否没有绑定上一轮证据；模糊输入是否仍无法导向交付级产品。

Cycle action:
本轮只改会影响 Goal / Loop 可执行性、意图对齐、prompt-only 边界、持续 LOOP 或镜像一致性的最高价值差距；不要为了显得完整新增 agent、hook 或无关流程。

Verification delta:
补跑镜像 hash、关键字段搜索、至少一个模糊人类意图样例，并说明本轮比上一轮多证明了什么。

Loop guardrails:
最多连续 3 个 LOOP 周期；若连续 2 轮仍无法让模糊意图样例产出合格 Goal + Loop、实机验证受模型缓存影响无法判断，或修改开始扩大到无关机制，则 Pause。

Continuation protocol:
每轮结束判定 `Done`、`Continue` 或 `Pause`。若仍有会影响交付级 Goal / Loop 的差距，输出下一轮 `Next LOOP packet`；如果实测受运行环境、模型缓存或用户偏好影响无法判断，暂停说明证据边界。

Stop / escalate conditions:
需要改变 prompt-only 边界、创建新 agent/hook、修改安装路径、提交发布或依赖未验证运行时时暂停。

Next LOOP packet:
包含原始改造目标、当前轮次、已关闭证据、开放差距、下一轮焦点、要读取的文件、验证入口和暂停条件。
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
下面是可直接复制的 Goal Prompt：

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

下面是交付后继续进化用的 Loop Prompt：

```markdown
Loop mission:
持续推进 GoalPro 输出质量，使它稳定地把模糊请求转成可执行、可验证、可暂停的 Goal Prompt，并附带可持续循环的 Loop Prompt。

Loop state:
继承上一轮输出、用户反馈、已关闭证据、开放差距、下一轮焦点和执行授权边界。

Previous result to inspect:
上一轮最终回复、生成的 Goal Prompt、Loop Prompt、用户反馈和任何验证证据。

Review evidence:
检查提示词是否只停在聊天输出、是否没有创建文件、是否能直接复制、是否有清楚的验收和暂停条件。

Gap diagnosis:
找出仍会导致执行者跑偏、过度规划、假完成或误把 GoalPro 当执行器的差距。

Cycle action:
本轮只调整提示词契约和输出形状中最高价值的差距；没有用户授权时，不改项目文件、不运行命令、不提交。

Verification delta:
用一个新的模糊请求样例验证输出是否仍能保持 Goal + Loop 双提示词。

Loop guardrails:
最多连续 3 个 LOOP 周期；若连续 2 轮仍出现执行越权、输出缺字段或 meta 包装污染，暂停重写上游 Goal 而不是继续局部修。

Continuation protocol:
每轮结束判定 `Done`、`Continue` 或 `Pause`。若仍有会导致跑偏或假完成的差距，输出下一轮 `Next LOOP packet`；如果用户意图不清到会改变输出位置或执行授权，暂停问用户。

Stop / escalate conditions:
用户要求保存/执行/提交、输出位置改变、权限边界改变或需要真实项目验证时暂停。

Next LOOP packet:
说明本轮收敛了哪些差距、还剩哪些风险、下一轮焦点、要检查的输出和停止条件。
```

你可以使用 LOOP 继续进行进化；每轮把上轮产出的 `Next LOOP packet` 带到下一轮。
````

## 文件加聊天双输出

输入：

```text
把这个目标保存到 docs/goals/optimize-goal-skill.md，也在聊天里给我一份可复制版本。
```

输出必须同时满足：

- 写入用户指定文件，或使用 `docs/goals/<topic>.md`。
- 聊天窗口同步输出同一份 Goal Prompt + Loop Prompt fenced `markdown` 代码块。
- 最后说明文件路径。

````markdown
已写入：`docs/goals/optimize-goal-skill.md`

聊天窗口可复制版本：

Goal Prompt:

```markdown
Goal:
[完整 Goal Contract 内容]

Intent:
[完整 Intent 内容]

Verification:
[完整 Verification 内容]
```

Loop Prompt:

```markdown
Loop mission:
[完整 Loop mission 内容]

Loop state:
[完整 Loop state 内容]

Previous result to inspect:
[完整 Previous result to inspect 内容]

Loop guardrails:
[完整 Loop guardrails 内容]

Stop / escalate conditions:
[完整 Stop / escalate conditions 内容]

Continuation protocol:
[完整 Continuation protocol 内容]

Next LOOP packet:
[完整 Next LOOP packet 内容]
```

你可以使用 LOOP 继续进行进化；每轮把上轮产出的 `Next LOOP packet` 带到下一轮。
````

## 模糊产品请求 + LOOP 示例

输入：

```text
帮我做个网站
```

合格输出要主动把“网站”放大成交付级产品，而不是只生成页面草稿：

````markdown
Goal Prompt:

```markdown
Goal:
做出一个可本地运行、可截图验收、适配桌面和移动端的网站首版；如果用户没有给品牌、行业或内容，先用最小可逆默认假设交付一个可替换内容的真实页面。

Intent:
用户表面上要“网站”，真实意图通常是想看到一个能拿来展示、评估或继续迭代的成品，而不是空模板、组件堆叠或营销话术。

Strategic outcome:
交付后用户能打开页面、看到清晰主题、主要内容、关键行动入口和基础响应式体验，并能基于真实截图继续提出修改。

Decision standard:
可见成品 > 用户意图贴合 > 响应式与可用性 > 可维护结构 > 视觉 polish。没有素材时使用明确默认假设，不捏造品牌事实。

Evidence standard:
先读项目现有技术栈、设计约定、运行脚本和资源文件；完成后提供本地运行 URL、桌面/移动截图或等价视觉验证、构建/类型检查结果。

Scope:
首屏、核心内容区、行动入口、基础导航、响应式布局、可替换文案和必要视觉资产。

Non-goals:
登录、支付、后台 CMS、SEO 全量策略、部署、真实品牌事实采集，除非用户明确要求。

Context to read first:
README、package scripts、现有页面入口、样式系统、资源目录、AGENTS/CLAUDE 规则。

Execution policy:
若项目已有前端框架和设计系统，沿用现有模式直接实现；若没有项目上下文，交付一个最小可运行静态站点并说明默认假设。若目标行业、品牌或功能会改变信息架构，最多问一个阻塞问题。

Verification:
页面能本地打开；桌面和移动视口无明显重叠；主要按钮/链接状态清楚；构建或静态检查通过；最终报告包含截图/URL/改动文件/剩余假设。

Stop conditions:
需要购买域名、接入支付、使用真实商标素材、采集个人数据、发布线上或选择互斥业务方向时暂停。

Final report:
用短报告说明默认假设、交付内容、验证证据、未做事项和下一步建议。
```

Loop Prompt:

```markdown
Loop mission:
持续推进网站首版达到“可展示、可验收、可继续迭代”的交付级状态；每轮关闭最影响用户判断网站方向的差距。

Loop state:
继承原始网站目标、当前轮次、已完成页面、已通过验证、开放差距、用户反馈、默认假设和下一轮焦点。

Previous result to inspect:
上一轮最终报告、本地 URL、桌面/移动截图、构建/检查输出、页面 diff、用户反馈和未解决假设。

Review evidence:
检查页面是否真实可打开、首屏是否表达明确主题、移动端是否无重叠、按钮是否可理解、截图是否证明结果，而不是只看“已完成”文字。

Gap diagnosis:
按阻塞访问、布局破损、意图不清、内容空泛、视觉粗糙、验证缺失排序剩余差距。

Cycle action:
本轮只修复影响交付级首版的最高价值差距；不要扩展登录、支付、后台、部署或复杂增长功能。若用户反馈改变行业/品牌/功能方向，先重写 Goal 再执行。

Verification delta:
补充上一轮缺失的运行、截图、构建或视口验证，并说明本轮新增证据关闭了哪些差距。

Loop guardrails:
最多连续 3 个 LOOP 周期；若连续 2 轮仍无法打开页面、截图/构建验证不可得、用户方向冲突或开放差距不减少，则 Pause。

Continuation protocol:
每轮结束判定 `Done`、`Continue` 或 `Pause`。若网站仍有影响交付级首版的开放差距，必须输出下一轮 `Next LOOP packet`；如果没有可运行环境、截图工具失败或用户方向冲突，暂停说明证据边界。

Stop / escalate conditions:
需要线上发布、第三方账号、真实品牌授权、付费素材、个人数据或不可逆改动时暂停。

Next LOOP packet:
包含原始网站目标、当前轮次、已关闭差距、开放差距、下一轮焦点、要读取的截图/URL/diff/反馈、验证 delta 和暂停条件。
```

你可以使用 LOOP 继续进行进化；每轮把上轮产出的 `Next LOOP packet` 带到下一轮。
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

交付后 Loop Prompt：

```markdown
Loop mission:
持续推进 TypeScript 迁移，直到项目获得可维护的类型基础，并且行为兼容、验证可信。

Loop state:
继承原始迁移目标、当前轮次、已迁移范围、已通过验证、开放类型差距、剩余 any、下一轮切片和暂停风险。

Previous result to inspect:
最终报告、tsconfig、迁移 diff、build/test 输出、显式 any 列表、用户反馈。

Review evidence:
区分 strict 编译通过、测试通过、显式 any 合理性说明和未验证声明。

Gap diagnosis:
优先关闭编译失败、行为回归、无说明 any、未迁移入口和验证缺口。

Cycle action:
不扩大到功能重写；每轮只处理最高价值且能验证的一组类型差距。

Verification delta:
说明本轮比上一轮多通过了哪些编译、测试或类型覆盖证据。

Loop guardrails:
最多连续 3 个 LOOP 周期；若连续 2 轮仍无法减少编译错误/显式 any/验证缺口，或需要依赖升级、行为改动、架构迁移，则 Pause。

Continuation protocol:
每轮结束判定 `Done`、`Continue` 或 `Pause`。若仍有未关闭且可验证的类型差距，输出下一轮 `Next LOOP packet`；依赖升级、行为改动或验证不可运行时暂停。

Stop / escalate conditions:
需要升级依赖、改变公共 API、修改运行时行为、放宽 strict 策略或验证命令不可运行时暂停。

Next LOOP packet:
列出原始迁移目标、当前轮次、已关闭差距、剩余 any、下一轮切片、要读取的文件、验证命令和暂停条件。
```

## Claude Code 任务提示词示例

```markdown
使用 goalpro Skill，把下面请求整理成可执行任务；目标清楚后再实现。

先读 `CLAUDE.md` 和用户点名文件。若请求依赖外部事实、战略判断或高质量研究，先做 deep research 并给证据地图；若存在会改变范围、风险或验收的多条路线，先通过原生提问界面问我。

若请求涉及大改、重构或跨模块行为，先输出 inventory 和分片验证计划，不要直接修改代码。

请求：
[用户请求]
```

交付后提醒：你可以把执行结果和 Loop Prompt 一起发给 Agent，继续进行进化；后续每轮用上轮产出的 `Next LOOP packet` 接着跑。
