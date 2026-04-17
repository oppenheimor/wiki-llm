# Superpowers

> 面向编程 Agent 的方法论型插件，把 brainstorm、plan、debug、TDD、review 等软件工程流程固化为可自动触发的 skills 组合。

## 核心能力
- **强制流程化开发**：在写代码前先做 brainstorming、design、planning，而不是直接进入实现。
- **方法论技能包**：内置 systematic-debugging、test-driven-development、requesting-code-review、using-git-worktrees 等工作流 skill。
- **支持 subagent 驱动开发**：可把任务拆成更小单元，由独立 subagent 执行并回收结果。
- **跨宿主可安装**：除 Claude Code 外，也支持 Codex CLI、Cursor、OpenCode、Gemini CLI 等环境。

## 技术亮点
### 它卖的不是“多几个命令”，而是“先想后做”的默认行为
Superpowers 的核心价值不在单个 skill，而在于把一套工程纪律变成默认路线。编码 Agent 遇到模糊需求时，不再立刻改代码，而是先澄清需求、收敛设计、再执行。

### Skills 组合成方法学，而不是插件杂货铺
Git worktree、code review、TDD、debugging、parallel agents 等能力被组织成一条可重复执行的流水线。这让它更像一层“Agent 开发操作系统”，而不是一组彼此独立的小命令。

## 使用场景
- 需要把“先设计、再实现、再验证”变成硬约束的编码工作
- 多人或长周期任务里，希望减少随意性与中途漂移
- 想把软件工程纪律以 skill 形式外包给 Agent Runtime

## 关联页面
- [[concepts/claude-code-skills]]
- [[concepts/skill-system]]
- [[concepts/harness-engineering]]
- [[patterns/llm-coding-discipline]]
- [[products/gstack]]

## 参考来源
- GitHub README：https://github.com/obra/superpowers（2026-04-17 查阅）
- 用户输入文章《实战篇: Claude Code + superpowers + gstack 开发流程实录，可直接复制使用，一篇文章讲清楚！》（2026-04-17 收录）
