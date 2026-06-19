# Goal Skill 方法依据

这个文件只在改进 Skill、解释方法来源、做质量复查时读取。普通使用不要加载。

## 采用的规则

- Goal 是完成契约，不只是提示词：必须写清结果、限制、done-when 和验证证据。
- Skill 的 `description` 是触发表面：只写“何时使用”和“做什么”，不能把次级优化目标写成触发词。
- 输出位置是用户体验契约：默认聊天窗口给可复制代码块；只有用户明确要求保存或提交时才写文件。
- Skill 正文要短；细节、来源、示例放 `references/`，靠 progressive disclosure 按需加载。
- 战略任务必须先证据后定论：没有 deep research 的战略只能标为草案。
- 复杂研究用 orchestrator-workers 思路拆源、拆观点、拆反证；有清晰评价标准时用 evaluator-optimizer 思路反复修正。
- 评测要拆开：意图识别、证据质量、路线判断、工具选择、执行遵守、最终状态不能混在一起。
- 开源与社区资料只作为实践信号：GitHub 优先于 X / Reddit；重复出现且能解释真实失败的信号才吸收。
- Meta_Kim：Critical -> Fetch -> Thinking -> Execution -> Review -> Verification；先取证再定路线；结构检查不能冒充用户目标完成。

## Deep Research 规则

当任务影响战略、路线、投入、长期标准，或依赖当前外部事实时，必须先做 deep research。

合格的 deep research 不是“搜很多链接”，而是形成可决策的证据地图，并让证据改变 Goal Contract。

执行流程：

1. `定义研究问题`：写清这次研究要改变哪个判断。不要写成宽泛主题。
   - 错误：研究 Claude Code 最佳实践。
   - 正确：判断 goalpro Skill 是否应该默认聊天输出，还是默认写入文件。
2. `拆子问题`：从事实、规范、实践、失败、反证、决策影响里选 3-7 个。
   - 事实问题：当前工具或平台到底支持什么？
   - 规范问题：官方文档建议怎么做？
   - 实践问题：高质量 GitHub 项目怎么组织？
   - 失败问题：用户真实踩坑是什么？
   - 反证问题：什么证据会推翻当前路线？
   - 决策问题：证据会改变 Goal 的哪个字段？
3. `分来源层级`：
   - `official`：最高权重，用于确认能力、规则、限制。
   - `local`：最高相关性，用于决定本项目怎么落地。
   - `github`：高权重，用于观察结构、维护方式、issue / discussion。
   - `paper / standard`：中高权重，用于研究质量、证据等级、报告结构。
   - `reddit`：中权重，用于发现失败模式和用户困惑。
   - `x`：低到中权重，用于发现趋势信号，必须交叉验证。
4. `检索取证`：
   - 每个关键子问题至少找 2 类来源。
   - 当前事实优先官方文档。
   - 本地落地优先项目文件。
   - 实践模式优先 GitHub。
   - 失败模式优先 issue / Reddit。
   - 热门观点必须找反例，不能只找支持材料。
   - 来源冲突时保留冲突，不强行合并。
5. `填写 Evidence Map`：每条证据都必须写成 claim，而不是复制长文。

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

6. `反证检查`：输出最终 Goal 前必须问：
   - 有没有来源说明这条路线会失败？
   - 有没有用户场景不适合这条规则？
   - 有没有官方文档和社区实践冲突？
   - 有没有本地项目现实让外部最佳实践不适用？
   - 如果反证成立，Goal 哪一部分要改？
7. `信心等级`：
   - `high`：官方/本地证据一致，且社区实践没有明显反例。
   - `medium`：多来源支持，但缺少本地验证或存在部分反例。
   - `low`：主要来自单个帖子、单个项目、推测或未验证经验。
8. `输出形态`：
   - 证据足够：输出 `Research-backed Goal Contract`。
   - 证据不足但方向清楚：输出 `Draft Goal`，标明缺口。
   - 关键证据缺失：输出 `Research Plan`，不要假装已经能定战略。
   - 路线冲突：输出候选路线对比和推荐默认，不直接执行。
9. `写回 Goal`：Deep Research 结果必须进入 Goal 字段。
   - 进入 `Decision standard`：改变优先级和取舍。
   - 进入 `Evidence standard`：规定后续还要验证什么。
   - 进入 `Scope / Non-goals`：明确做什么、不做什么。
   - 进入 `Execution policy`：决定直接做、先问、先 inventory 还是暂停。
   - 进入 `Verification`：定义怎么证明完成。
   - 进入 `Stop conditions`：定义哪些风险必须停。

如果研究没有改变成败标准、边界、执行策略或验证方式，就不算 deep research。

## GitHub / X / Reddit 吸收规则

三类来源的权重不同：

- `GitHub repo / discussion`：可观察到文件结构、实践约定、issue 讨论和维护方式，适合抽象成规则。
- `Reddit thread`：适合发现真实用户困惑、失败模式和反例，不适合单独作为权威。
- `X post / article`：适合捕捉新实践和短工作流口号，必须用 GitHub、官方文档或本地验证交叉确认。

可吸收的社区信号：

1. `Context layering`：常驻文件只放核心规则，细节放 references/docs，按需读取，防止上下文污染。
2. `Inventory before mutation`：大改、重构、复杂代码任务先列影响文件、调用方、测试和验证入口。
3. `Plan as artifact`：复杂计划应写成可编辑、可恢复的 Markdown，而不是只留在对话历史。
4. `Small step verification`：每个阶段都要有最小相关检查，最后再做完整验证。
5. `Skill / command / agent boundary`：Skill 放可复用流程；agent 放独立上下文和工具权限；command 放显式触发动作。
6. `Reload awareness`：运行中的会话可能缓存 skill / agent 定义；修改定义后不能只靠同一会话自测证明新定义生效。

拒绝吸收的社区信号：

- 只是一句流行口号，无法改变成败标准。
- 只对某个作者的私有工具链成立。
- 要求所有任务走重流程，导致小任务过度规划。
- 鼓励把所有东西塞进 `CLAUDE.md` / `AGENTS.md`。
- 用更多 agent、hook、MCP 掩盖意图不清。

## 质量原则

1. 意图放大优先：不能只复述用户原话，要说清真实意图和战略结果。
2. 完成度优先：成败标准、关键边界、证据路径和取舍逻辑必须清楚。
3. 证据优先：战略和外部事实任务必须有来源、反证、信心等级和决策影响。
4. 表达经济从属：只删空话，不删判断、边界、标准、验证。
5. 每个关键字段必须能判断合格/不合格。
6. 输出位置必须可预期：聊天默认、文件显式、文件模式也给聊天代码块。
7. 上下文读取只列会改变路线或验收的材料。
8. 验证必须区分：未验证、结构检查、本地验证、线上验证、人工验收。
9. 不因“看起来完整”增加机制；只为防真实失败加规则。
10. 社区经验要过来源权重和反证筛选，不能把热闹观点写成标准。

## 来源地图

- YAO Meta Skill: https://github.com/yaojingang/yao-meta-skill
- Agent Skills spec: https://agentskills.io/specification
- Agent Skills best practices: https://agentskills.io/skill-creation/best-practices
- OpenAI Codex prompting and goals: https://developers.openai.com/codex/prompting
- OpenAI Codex follow goals: https://developers.openai.com/codex/use-cases/follow-goals
- OpenAI Codex skills best practices: https://developers.openai.com/codex/skills
- OpenAI Deep Research API: https://developers.openai.com/api/docs/guides/deep-research
- OpenAI Deep Research cookbook: https://developers.openai.com/cookbook/examples/deep_research_api/introduction_to_deep_research_api
- OpenAI Academy Deep Research guide: https://academy.openai.com/public/clubs/work-users-ynjqu/resources/integrating-deep-research-into-your-workflow-2026-05-29
- Claude Code skills: https://code.claude.com/docs/en/skills
- Claude Agent Skills overview: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/overview
- Claude Agent Skills best practices: https://platform.claude.com/docs/en/agents-and-tools/agent-skills/best-practices
- Anthropic skill-creator: https://docs.anthropic.com/en/docs/claude-code/skill-creator
- Anthropic Building Effective Agents: https://www.anthropic.com/engineering/building-effective-agents
- Anthropic agent evaluation: https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents
- PRISMA 2020: https://www.prisma-statement.org/prisma-2020
- GRADE approach: https://www.gradeworkinggroup.org/
- AGENTS.md format: https://github.com/agentsmd/agents.md
- Addy Osmani agent-skills: https://github.com/addyosmani/agent-skills
- mgechev skills-best-practices: https://github.com/mgechev/skills-best-practices
- ykdojo Claude Code tips: https://github.com/ykdojo/claude-code-tips
- ching-kuo claude-codex workflow: https://github.com/ching-kuo/claude-codex
- shinpr codex-workflows: https://github.com/shinpr/codex-workflows
- OpenAI Codex plan/spec discussion: https://github.com/openai/codex/discussions/7355
- Reddit AGENTS.md practice thread: https://www.reddit.com/r/ChatGPTCoding/comments/1nwe5nz/my_agentsmd/
- Reddit large-codebase agent workflow thread: https://www.reddit.com/r/ClaudeCode/comments/1rwojpn/best_approach_to_use_ai_agents_claude_code_codex/
- Reddit Claude.md / skills / agents structure thread: https://www.reddit.com/r/ClaudeCode/comments/1qub3fm/best_practices_project_structure_ie_interplay/
- Reddit goal-driven CLAUDE.md thread: https://www.reddit.com/r/ClaudeAI/comments/1t89g1j/best_claudemd_files_for_claude_code/
- X workflow signal, scoped workflows: https://x.com/trq212/status/2061907538741006796
- X plan artifact signal: https://x.com/derrickcchoi/status/2031023512534634758
- X smallest verification signal: https://x.com/PaulSolt/article/2040132557983936772
- X plan-validate-execute signal: https://x.com/nurijanian/article/2060672098050490380

## 来源抽象

- OpenAI Codex goal 文档：goal 要像“完成条件”一样写，包含具体结果、可测标准和验证面。
- OpenAI / Agent Skills / Claude Skills：Skill 触发主要依赖 frontmatter description；description 必须描述使用场景，不能塞次要目标。
- OpenAI Deep Research：适合陌生、高风险、证据密集的任务；输出应带引用、来源元数据和中间检索过程。
- Anthropic agents：复杂研究可拆成多个子问题；有明确评价标准时，应让评估反过来改进结果。
- PRISMA / GRADE：高质量研究要说明为什么做、怎么找、证据有多可靠，以及证据如何支持建议强度。
- GitHub 社区项目：高质量 Skill 倾向于单一职责、可验证退出条件、短正文和按需 references；复杂工作流常见 plan -> implement -> review 或 plan -> diff -> verify。
- Reddit 真实反馈：用户最常遇到的是上下文污染、计划文件缺失、过度使用 agent/hook/MCP、先改后盘点、验证不连续。
- X 实践信号：新工作流常把计划、diff、验证、最小测试和隔离上下文当作短循环，但这些只能作为候选模式，必须交叉验证。
- Meta_Kim：Critical/Fetch/Thinking/Review 是路线约束；没有 Fetch 的战略判断不能假装完成。

## 反模式

- “做得更好”但没有用户、目标和验收。
- 不做 deep research 就给战略结论。
- 把表达成本写进 `description`，污染触发判断。
- 把缩短提示词当核心目标，牺牲意图放大和战略完成度。
- 列任务很多，却没有最终状态。
- 把 Reddit/X 单帖当权威结论。
- 先重构再补 inventory。
- 把计划只留在聊天历史，导致恢复和验收不可见。
- 用户只要 goal / prompt，却默认写文件、更新图谱或提交 git。
- 写了文件后，只给路径不给聊天窗口可复制代码块。
- 不区分 Skill、command、agent，把所有能力混成一个大提示词。
- 用户给了文件/错误/截图，却先问一堆问题。
- 小任务要求全仓库阅读。
- 测试通过就说完成，但用户要的行为没有证据。
- 为了显得高级创建 Skill、agent、command、eval。
