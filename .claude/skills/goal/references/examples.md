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

Outcome:
已有用户能用账号密码登录，并获得受保护会话。

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

## Codex `/goal` 示例

```markdown
/goal
把项目从 JavaScript 迁移到 TypeScript。

Done when:
- 应用能在 strict mode 下编译。
- 不新增显式 `any`。
- 现有用户行为不变。

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

先读 `CLAUDE.md` 和用户点名文件。若存在会改变范围、风险或验收的多条路线，先通过原生提问界面问我。

请求：
[用户请求]
```
