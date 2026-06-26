# Changelog

## v0.1.2 - 2026-06-26

Adds a workflow lens to GoalPro so repeated automation-style requests become safer, clearer Goal + Loop contracts without turning every task into a workflow.

### Changed

- Add `Workflow lens` guidance for recurring work such as daily, weekly, automatic, publishing, operations, monitoring, queues, review, and sync tasks.
- Teach GoalPro to add `Trigger`, `Checkpoint`, `Brief`, and source-of-truth guidance only when a request is genuinely repeatable.
- Strengthen the one-question rule: route-changing ambiguity should ask one blocking question with a recommended answer, while context-answerable questions should be resolved by reading context.
- Update the Xiaohongshu publisher example to model a safe publishing workflow with late human confirmation, decision briefs, and clear non-automation boundaries.
- Clarify that one-off website work should not be forced into workflow form unless the user asks for ongoing feedback, updates, operations, or measurement.
- Mirror all Skill, source-rules, and examples changes across `.agents` and `.claude`.

### Verification

- `git diff --check` passed with only LF-to-CRLF warnings.
- `.agents` and `.claude` GoalPro skill mirrors have matching SHA256 hashes for `SKILL.md`, `references/source-rules.md`, and `references/examples.md`.
- Key workflow-lens fields were checked with `rg`, including `Workflow lens`, `Trigger`, `Checkpoint`, `Brief`, `推荐答案`, and `小红书自动发布器`.
- `graphify update .` completed after the workflow-lens update.

## v0.1.1 - 2026-06-26

Improves GoalPro's Loop Prompt contract and adds concrete, user-judgeable examples for automation-heavy fuzzy product requests.

### Changed

- Front-load `时间参数` in Loop Prompt guidance while keeping automation setup as a separately authorized step.
- Strengthen completion reporting so final reports include a judgeable sample or case snippet, not just validation claims.
- Refine Loop rules around evidence review, intent amplification, automation readiness, and stop or escalation boundaries.
- Add a full Xiaohongshu publisher example that requires deep research before implementation and distinguishes publishing assistance from unsafe or unverified automation.
- Mirror all GoalPro Skill, source-rules, and examples changes across `.agents` and `.claude`.

### Verification

- `git diff --check` passed with only LF-to-CRLF warnings.
- `.agents` and `.claude` GoalPro skill mirrors have matching SHA256 hashes for `SKILL.md`, `references/source-rules.md`, and `references/examples.md`.
- Key fields and examples were checked with `rg`, including `时间参数`, `验收样例`, and `我需要小红书自动发布器`.
- `graphify update .` completed after the example update.

## v0.1.0 - 2026-06-26

GoalPro's first GitHub release formalizes the upgrade from a single Goal Contract generator into a dual-prompt Skill for execution and continued improvement.

### Changed

- Reframed GoalPro around `Goal Prompt + Loop Prompt` across the README and both runtime skill copies.
- Kept the prompt-only boundary explicit: GoalPro generates copyable prompts, but does not execute the goal or run the loop without separate user authorization.
- Added Loop fields for evidence review, gap diagnosis, verification delta, guardrails, Done / Continue / Pause decisions, and `Next LOOP packet` handoff.
- Expanded examples for login, strategic research, file + chat output, fuzzy website requests, TypeScript migration, and Claude Code task prompts.
- Updated source rules to connect iterative improvement with evidence, loop state, no-progress thresholds, and stop/escalation conditions.
- Ignored `.claude/project-task-state.json` so local Claude task state stays out of Skill releases.

### Verification

- `.agents` and `.claude` GoalPro skill mirrors have matching SHA256 hashes for `SKILL.md`, `references/source-rules.md`, and `references/examples.md`.
- Static diff inspection confirms the release scope is limited to GoalPro docs, skill rules, examples, and release notes.
- `graphify query` was used before release-oriented source inspection, following the repo's graph-first navigation rule.
