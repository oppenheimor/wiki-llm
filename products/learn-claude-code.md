# Learn Claude Code

> 一个 0→1 教学项目，通过 12 个渐进式课程（s01-s12）系统讲解 Agent Harness（智能体 infrastructure）的工程构建方法。

## 核心命题

**Agency（智能）来自模型训练，而非外部代码编排。** 模型是司机，Harness 是车辆。一个完整的 Agent Product = Model + Harness。

仓库标题 "Bash is all you need" 表达的正是这个理念：最简 Agent Loop 只需要一个 `while` + `stop_reason` 判断，剩下的就是执行模型想要的工具调用。

## 核心概念：Harness Engineering

Harness 是智能体在特定领域工作所需的全部基础设施：

```
Harness = Tools + Knowledge + Observation + Action Interfaces + Permissions

    Tools:          file I/O, shell, network, database, browser
    Knowledge:      product docs, domain references, API specs, style guides
    Observation:    git diff, error logs, browser state, sensor data
    Action:         CLI commands, API calls, UI interactions
    Permissions:    sandboxing, approval workflows, trust boundaries
```

仓库的核心理念：工程师的工作不是写智能，而是构建智能居住的世界。

## 12 个课程阶段

### Phase 1: The Loop（基础循环）
- **s01** — Agent Loop：one loop + stop_reason
- **s02** — Tool Use：dispatch map 注册机制

### Phase 2: Planning & Knowledge（规划与知识）
- **s03** — TodoWrite：任务分解 + nag reminder
- **s04** — Subagents：独立 messages[] 隔离
- **s05** — Skills：按需加载知识（SKILL.md via tool_result）
- **s06** — Context Compact：三层压缩策略

### Phase 3: Persistence（持久化）
- **s07** — Tasks：基于文件的 CRUD + 依赖图
- **s08** — Background Tasks：daemon 线程 + 通知队列

### Phase 4: Teams（多智能体协作）
- **s09** — Agent Teams： teammates + JSONL mailboxes
- **s10** — Team Protocols：shutdown + plan approval FSM
- **s11** — Autonomous Agents：idle cycle + auto-claim
- **s12** — Worktree Isolation：任务协调 + 隔离执行目录

## 与 Claude Code 的关系

仓库选择 Claude Code 作为教学对象，因为它是"最优雅、最充分实现的 Agent Harness"。

Claude Code 的本质架构：
```
Claude Code = one agent loop
            + tools (bash, read, write, edit, glob, grep, browser...)
            + on-demand skill loading
            + context compression
            + subagent spawning
            + task system with dependency graph
            + team coordination with async mailboxes
            + worktree isolation for parallel execution
            + permission governance
```

 lesson 是：**最好的 Agent 产品由理解"工程师的职责是 harness 而不是智能"的工程师构建。**

## 体系定位

与 [[products/everything-claude-code]] 的关系：
- ECC 是现有配置仓库的使用和扩展
- Learn Claude Code 是从零理解 harness 工程原理的教程

两者是互补的：
- ECC 告诉你"怎么用"
- Learn Claude Code 告诉你"怎么实现"

## 关联页面

- [[products/everything-claude-code]] — 现有配置仓库（四层架构）
- [[concepts/agent-loop]] — 课程 s01 对应的最小调度内核
- [[concepts/react-pattern]] — “想-做-看”认知闭环的理论表达
- [[concepts/claude-code-routines]] — 云端自动化（s07-s12 的云端版本）
- [[concepts/claude-code-agents]] — sub-agent 机制（s04 的对应概念）
- [[concepts/claude-code-skills]] — skill 机制（s05 的对应概念）
- [[concepts/hermes-agent]] — 对比：另一个自托管 Agent 框架
- [[concepts/openclaw]] — Sister repo：从 always-on harness 到IM通道+memory+soul personality

## 参考来源

- GitHub：https://github.com/shareAI-lab/learn-claude-code
- 仓库 README（通过 Jina 抓取，2026-04-15）
