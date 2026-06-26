# Changelog

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
