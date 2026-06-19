# Goal Skill 方法依据

这个文件只在改进 Skill、解释方法来源、做质量复查时读取。普通使用不要加载，省 Token。

## 采用的规则

- YAO Meta Skill：`SKILL.md` 保持短；触发靠 frontmatter；细节放 `references/`；重复场景和稳定输出契约才值得做 Skill。
- Agent Skills specification：`name` 和 `description` 是常驻触发表面；正文要短，靠 progressive disclosure 加载细节。
- Codex：好 goal 必须包含目标、上下文、限制和 done-when；`/goal` 要有具体结果或测试标准。
- Claude Code：持久项目事实放 `CLAUDE.md`；Skill 用于重复流程；只有并行或隔离上下文有价值时才用 subagent。
- Anthropic agent patterns：routing、orchestrator-workers、evaluator-optimizer、parallelization 都要满足适用条件，不能为了显得完整乱加。
- Agent 评测思想：把结果、过程、工具选择、工具调用、任务遵守、意图识别、最终状态分开评估。
- Spec-driven development：先写 what / why，再写 how；目标和验收标准比执行步骤更重要。
- Meta_Kim：Critical -> Fetch -> Thinking -> Execution -> Review -> Verification；先取证再定路线；结构检查不能冒充用户目标完成。

## 质量原则

1. Token 优先花在标准上，不花在解释包装上。
2. 每个字段必须能判断合格/不合格。
3. 上下文读取只列会改变路线或验收的材料。
4. 验证必须区分：未验证、结构检查、本地验证、线上验证、人工验收。
5. 不因“看起来完整”增加机制；只为防真实失败加规则。

## 来源地图

- YAO Meta Skill: https://github.com/yaojingang/yao-meta-skill
- Agent Skills spec: https://agentskills.io/specification
- Agent Skills best practices: https://agentskills.io/skill-creation/best-practices
- OpenAI Codex best practices: https://developers.openai.com/codex/learn/best-practices
- OpenAI Codex prompting and goals: https://developers.openai.com/codex/prompting
- OpenAI Codex follow goals: https://developers.openai.com/codex/use-cases/follow-goals
- Claude Code skills: https://docs.anthropic.com/en/docs/claude-code/skills
- Claude Code subagents: https://docs.anthropic.com/en/docs/claude-code/sub-agents
- Anthropic Building Effective Agents: https://www.anthropic.com/engineering/building-effective-agents
- Anthropic agent evaluation: https://www.anthropic.com/engineering/demystifying-evals-for-ai-agents
- Microsoft agent evaluators: https://learn.microsoft.com/en-us/azure/foundry/concepts/evaluation-evaluators/agent-evaluators
- Addy Osmani on AI-agent specs: https://addyosmani.com/blog/good-spec/
- Martin Fowler on spec-driven development: https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html
- GitHub Spec Kit: https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/

## 反模式

- “做得更好”但没有用户、目标和验收。
- 列任务很多，却没有最终状态。
- 用户给了文件/错误/截图，却先问一堆问题。
- 小任务要求全仓库阅读。
- 测试通过就说完成，但用户要的行为没有证据。
- 为了显得高级创建 Skill、agent、command、eval。
