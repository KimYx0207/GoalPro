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
改动文件、行为变化、验证结果、剩余风险，并展示一个登录成功/失败路径的样例片段，方便用户判断是否通过。
```

Loop Prompt:

```markdown
时间参数:
请自行填写 LOOP 时间，如“每天早上 09:00”；如果只想手动继续，填写“手动：贴入上一轮报告、验证输出或 Next LOOP packet 后继续”。

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
包含原始登录目标、当前轮次、已关闭证据、开放差距、时间参数、下一轮焦点、要读取的材料、暂停条件和本轮新增验证。
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
时间参数:
请自行填写 LOOP 时间，如“每周一 09:00”；如果只想手动继续，填写“手动：贴入上一轮改造结果、验证证据或 Next LOOP packet 后继续”。

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
包含原始改造目标、当前轮次、已关闭证据、开放差距、时间参数、下一轮焦点、要读取的文件、验证入口和暂停条件。
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
时间参数:
请自行填写 LOOP 时间，如“每天早上 09:00”；如果只想手动继续，填写“手动：贴入上一轮输出、反馈或 Next LOOP packet 后继续”。

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
说明本轮收敛了哪些差距、还剩哪些风险、时间参数、下一轮焦点、要检查的输出和停止条件。
```

按 `时间参数` 使用 LOOP 继续进化；如果要定时或后台自动跑，需要单独授权自动化设置。
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
时间参数:
[请自行填写 LOOP 时间，如“每天早上 09:00”；如果只想手动继续，填写“手动：贴入上一轮结果或 Next LOOP packet 后继续”]

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

按 `时间参数` 使用 LOOP 继续进化；如果要定时或后台自动跑，需要单独授权自动化设置。
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

Workflow lens:
默认不把“做个网站”当成 workflow；它先是一件交付首版的任务。只有用户提出持续更新、定期收集反馈、每天检查数据或内容运营时，才把后续维护写成 workflow。

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
用短报告说明默认假设、交付内容、验证证据、未做事项和下一步建议，并展示一个首屏/移动端/按钮状态的验收样例片段，让用户能判断网站是否过关。
```

Loop Prompt:

```markdown
时间参数:
请自行填写 LOOP 时间，如“每天早上 09:00 检查网站反馈”；如果只想手动继续，填写“手动：贴入上一轮截图、URL、反馈或 Next LOOP packet 后继续”。

Loop mission:
在网站首版交付后，用截图、URL、构建输出和用户反馈做复盘；每轮只关闭一个最影响“能展示、能判断、能继续改”的差距。

Loop state:
继承原始网站目标、当前轮次、已完成页面、已通过验证、开放差距、用户反馈、默认假设和下一轮焦点。

Previous result to inspect:
上一轮最终报告、本地 URL、桌面/移动截图、构建/检查输出、页面 diff、用户反馈和未解决假设。

Review evidence:
检查页面是否真实可打开、首屏是否表达明确主题、移动端是否无重叠、按钮是否可理解、截图是否证明结果，而不是只看“已完成”文字。

Gap diagnosis:
按阻塞访问、布局破损、意图不清、内容空泛、视觉粗糙、验证缺失排序剩余差距。

Cycle action:
本轮只修复影响网站首版判断的最高价值差距，例如打不开、移动端乱、首屏看不懂、按钮不清楚或截图证据缺失；不要扩展登录、支付、后台、部署或复杂增长功能。若用户反馈改变行业/品牌/功能方向，先重写 Goal 再执行。

Verification delta:
补充上一轮缺失的运行、截图、构建或视口验证，并说明本轮新增证据关闭了哪些差距。

Loop guardrails:
最多连续 3 个 LOOP 周期；若连续 2 轮仍无法打开页面、截图/构建验证不可得、用户方向冲突或开放差距不减少，则 Pause。

Continuation protocol:
每轮结束判定 `Done`、`Continue` 或 `Pause`。若网站仍有影响交付级首版的开放差距，必须输出下一轮 `Next LOOP packet`；如果没有可运行环境、截图工具失败或用户方向冲突，暂停说明证据边界。

Stop / escalate conditions:
需要线上发布、第三方账号、真实品牌授权、付费素材、个人数据或不可逆改动时暂停。

Next LOOP packet:
包含原始网站目标、当前轮次、已关闭差距、开放差距、时间参数、下一轮焦点、要读取的截图/URL/diff/反馈、验证 delta 和暂停条件。
```

按 `时间参数` 使用 LOOP 继续进化；如果要定时或后台自动跑，需要单独授权自动化设置。
````

## 平台自动化产品请求完整案例

输入：

```text
我需要小红书自动发布器
```

合格输出要把“自动发布器”拆成安全、合规、可验收的产品目标，而不是直接承诺绕过平台限制自动发帖：

````markdown
Goal Prompt:

```markdown
Goal:
做出一个合规优先的小红书内容发布辅助器 MVP：支持内容草稿、图片/视频素材、发布时间计划、发布前检查、人工确认发布或官方能力发布，并保留发布记录和失败原因。

Intent:
用户表面上要“小红书自动发布器”，真实意图通常是减少重复发布操作、统一管理内容日历、降低漏发/错发风险，而不是冒着账号风控风险做一个不可控的黑盒发帖机器人。

Strategic outcome:
交付后用户能把一批小红书内容从“散落文案和素材”变成可检查、可排期、可追踪的发布队列；如果平台允许官方发布能力，则走官方能力；如果不允许，则提供半自动发布辅助和人工确认流程，避免账号安全和合规风险。

Decision standard:
账号安全与平台规则 > 内容发布闭环 > 可追踪状态 > 自动化程度 > 界面 polish。不能为了“自动”绕过登录、验证码、风控、平台规则或用户确认。

Workflow lens:
这类需求按重复 workflow 处理。每轮从“新增草稿/到达检查时间/用户触发发布准备”开始，经过内容检查、风险提示、排期、发布前人工确认、状态记录和失败复盘；队列状态表是 source of truth。Checkpoint 要尽量后移到发布前，先把决策 Brief 准备好，再让用户做一次关键确认。

Evidence standard:
先核对项目技术栈、现有账号/内容/素材数据结构、目标发布流程，以及小红书官方开放平台/创作中心/平台规则中与发布、授权、内容管理相关的当前能力；完成后提供本地可运行入口、草稿到发布队列的演示数据、发布前检查样例、失败/暂停状态样例和安全边界说明。

Scope:
- 内容草稿管理：标题、正文、话题、图片/视频、封面、发布时间、账号标识。
- 发布队列：待检查、待确认、待发布、已发布、失败、暂停。
- 发布前检查：缺素材、标题过长、正文为空、敏感词占位、图片数量/格式占位检查。
- 发布 Brief：每条内容给出标题、素材状态、计划时间、风险、推荐动作和证据链接。
- 发布方式：优先官方 API/官方工具链；没有官方能力时，生成手动发布清单或半自动复制辅助。
- 发布记录：每条内容的状态、时间、操作者、失败原因、下一步动作。

Non-goals:
不绕过验证码/登录/风控；不模拟真人规避平台检测；不存储明文账号密码；不批量骚扰式发布；不承诺平台未开放的自动发布能力；不直接上线真实账号发布，除非用户明确授权并完成平台合规核对。

Context to read first:
README、package scripts、现有前后端入口、数据模型、任务/队列方案、环境变量示例、认证方案、素材存储目录、现有自动化/定时任务代码、项目里的平台集成约定。

Constraints:
不得打印或提交账号、cookie、token、短信验证码、私信内容或个人数据；所有真实发布动作必须有人工确认或官方授权证据；发布失败不能无限重试；涉及真实账号、真实内容、线上发布、代理或浏览器自动化时必须暂停确认。

Execution policy:
先做 inventory，确认是否已有账号模型、内容模型、队列系统和 UI 框架。若没有官方发布能力证据，默认交付“发布辅助器”：实现草稿、排期、检查、发布 Brief、人工确认和状态记录。若必须确认路线，只问一个阻塞问题并给推荐答案，例如“我建议默认走人工确认发布，因为官方发布能力和账号授权未确认；你同意吗？”只有在官方能力与用户授权都明确后，才接入真实发布动作。

Checkpoints:
1. 画出当前内容从草稿到发布的状态流转。
2. 实现最小数据结构和示例内容种子数据。
3. 实现列表/编辑/排期/检查/状态更新界面或接口。
4. 实现发布前检查、失败原因和发布 Brief 展示。
5. 将人工确认点后移到发布前：用户看到 Brief 后只确认发布、修改或暂停。
6. 真实自动发布能力留在明确授权后的独立步骤。

Verification:
用 2-3 条模拟小红书内容验证：一条检查通过进入待确认，一条因缺图片失败，一条因需要官方授权暂停。提供本地 URL 或命令输出、状态流转截图/表格、关键文件、未接入真实发布的说明和剩余风险。

Stop conditions:
需要真实小红书账号、cookie/token、验证码、代理池、浏览器自动登录、绕过风控、真实发布、批量私信/互动、采集用户数据或调用未确认的第三方灰色接口时暂停。

Final report:
汇报默认假设、实现范围、状态流转、验证结果、未做事项和风险边界，并展示一组完整验收样例：输入的 3 条内容、各自检查结果、发布状态、失败/暂停原因和下一步动作，让用户能判断是否通过。
```

Loop Prompt:

```markdown
时间参数:
请自行填写 LOOP 时间，如“每天早上 09:00 检查发布队列”；如果只想手动继续，填写“手动：贴入上一轮最终报告、截图、状态表、用户反馈或 Next LOOP packet 后继续”。

Loop mission:
持续推进小红书发布辅助器从“能管理草稿和发布队列”走向“安全、可追踪、可授权地减少人工发布成本”；每轮只关闭一个最影响发布闭环或账号安全的差距。

Loop state:
继承原始产品目标、当前轮次、已实现模块、发布方式假设、已验证状态流转、开放风险、用户反馈、平台能力核对状态和下一轮焦点。

Trigger:
优先事件触发：新草稿进入待检查队列、内容到达计划检查时间、用户手动点击准备发布；固定时间如“每天 09:00”只是时间参数，不代表已创建后台任务。

Checkpoint:
发布前只让用户做一次关键确认：确认发布、修改后再审、暂停并补授权。不要在还没准备好内容、素材、风险和推荐动作前打断用户。

Brief:
每条待确认内容必须给用户一个短摘要：标题、素材状态、计划发布时间、检查结果、风险、推荐动作、证据链接或截图位置。用户读 Brief，不读原始草稿堆。

Previous result to inspect:
上一轮最终报告、本地 URL/截图、内容状态表、模拟内容数据、发布 Brief、发布前检查输出、失败日志、平台能力核对结论、用户对自动化程度的反馈。

Review evidence:
区分“草稿管理可用”“发布前检查可用”“人工确认路径可用”“真实发布已授权且可用”和“只是界面写了自动发布”。不能把模拟状态当成真实平台发布成功。

Gap diagnosis:
按账号安全风险、平台能力不明、发布闭环缺口、状态不可追踪、检查规则缺失、界面效率低排序剩余差距。

Cycle action:
本轮只处理最高价值差距。若缺少官方发布能力证据，优先强化发布辅助和人工确认；若用户提供官方授权和测试账号，再单独设计真实发布接入；不要扩展到私信、评论、采集、涨粉或规避风控功能。

Verification delta:
补充上一轮缺失的状态流转、截图、Brief 样例、失败样例、授权边界或发布记录验证，并说明本轮新增证据关闭了哪些差距。

Loop guardrails:
最多连续 3 个 LOOP 周期；若连续 2 轮仍无法确认平台发布能力、真实账号授权不可得、测试发布风险过高、或用户要求绕过风控，则 Pause。

Continuation protocol:
每轮结束判定 `Done`、`Continue` 或 `Pause`。如果仍有影响安全发布闭环的开放差距，输出下一轮 `Next LOOP packet`；如果主要闭环已完成且风险边界清楚，报告 Done；如果需要真实账号、授权、平台规则判断或高风险自动化，报告 Pause。

Stop / escalate conditions:
需要真实账号登录、cookie/token、验证码、代理、浏览器模拟发布、绕过平台限制、真实上线发布、处理个人数据、调用不明第三方接口或批量互动时暂停。

Next LOOP packet:
包含原始小红书发布辅助器目标、当前轮次、已关闭证据、开放差距、时间参数、Trigger、Checkpoint、Brief 要求、下一轮焦点、要读取的状态表/截图/日志/平台能力证据、验证 delta 和暂停条件。
```

验收样例：

```markdown
模拟内容 A：标题、正文、3 张图片齐全 -> 状态：待人工确认发布 -> 下一步：用户确认或复制到官方发布入口。
模拟内容 B：正文齐全但缺图片 -> 状态：检查失败 -> 原因：缺少至少 1 张图片 -> 下一步：补素材。
模拟内容 C：计划每天 09:00 自动发布 -> 状态：暂停 -> 原因：未确认官方发布能力和账号授权 -> 下一步：核对官方能力或改为人工确认。
Brief 示例：内容 A 已通过检查，建议动作：确认发布；证据：3 张图片齐全、标题未超长、发布时间已设置。
```

按 `时间参数` 使用 LOOP 继续进化；如果要定时或后台自动跑，需要单独授权自动化设置。
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
时间参数:
请自行填写 LOOP 时间，如“每天晚上 22:00”；如果只想手动继续，填写“手动：贴入上一轮最终报告、build/test 输出或 Next LOOP packet 后继续”。

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
列出原始迁移目标、当前轮次、已关闭差距、剩余 any、时间参数、下一轮切片、要读取的文件、验证命令和暂停条件。
```

## Claude Code 任务提示词示例

```markdown
使用 goalpro Skill，把下面请求整理成可执行任务；目标清楚后再实现。

先读 `CLAUDE.md` 和用户点名文件。若请求依赖外部事实、战略判断或高质量研究，先做 deep research 并给证据地图；若存在会改变范围、风险或验收的多条路线，先通过原生提问界面问我。

若请求涉及大改、重构或跨模块行为，先输出 inventory 和分片验证计划，不要直接修改代码。

请求：
[用户请求]
```

交付后提醒：按 `时间参数` 把执行结果和 Loop Prompt 一起发给 Agent 继续进化；后续每轮用上轮产出的 `Next LOOP packet` 接着跑。若要定时或后台自动跑，需要单独授权自动化设置。
