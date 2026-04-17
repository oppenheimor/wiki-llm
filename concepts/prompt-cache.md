# Prompt Cache

> 通过缓存请求前缀对应的推理中间状态，避免每轮请求都重新处理相同提示词与工具定义的成本优化机制。

## 核心要点
- **缓存的是前缀，不是整段会话**：只有从请求开头开始、连续一致的那段内容才能命中缓存。
- **前缀稳定性决定成本结构**：system prompt、工具定义、缓存边界的布局，会直接影响长会话 Agent 的延迟和费用。
- **它约束了上下文压缩策略**：压缩消息历史时不能随意动缓存前缀，否则省下窗口，反而打烂缓存。
- **它是托管式 Agent 平台的重要计费杠杆**：当平台承担运行时编排时，prompt cache 命中率会成为实际可用性的关键一环。

## 详细说明
### 本质是“别重复算已经算过的前缀”
Prompt Cache 利用模型对长前缀重复处理的低效点，把 system prompt、工具定义等稳定输入对应的中间状态缓存下来。下次请求只要前缀完全一致，就可以直接复用。

### Cache-aware 的请求布局本身就是一种工程能力
高质量 Agent Runtime 不只是“会压缩上下文”，还要知道哪些内容必须稳定放在前面，哪些动态内容应该追加到后面。典型做法是把静态说明、工具定义放进可缓存前缀，把工作目录、日期、会话态和附件放到动态区。

### 它与上下文压缩是互补关系
Prompt Cache 解决的是重复计算成本，压缩解决的是窗口占用和注意力污染。两者目标不同，但会互相制约：如果压缩动作破坏了缓存边界，系统就可能在节省 token 的同时增加推理成本。

## 上下文
这类机制在 Claude Code 一类长会话编程 Agent 中尤其关键，因为同一个系统提示和工具集会被重复发送几十上百次。用户输入文章《Claude Code 上下文管理机制》把它明确呈现为运行时架构约束，而不只是 API 小技巧。

## 关联页面
- [[concepts/kv-cache]]
- [[concepts/token-efficiency]]
- [[concepts/harness-engineering]]
- [[products/claude-code-harness-analysis]]
- [[products/claude-agent-sdk]]
- [[products/claude-managed-agents]]

## 参考来源
- 用户输入文章《Claude Code 上下文管理机制》（2026-04-17 收录）
- 用户输入文章《Anthropic 官方 Agent Harness 平台：Claude Managed Agents 完整指南》（2026-04-17 收录）
