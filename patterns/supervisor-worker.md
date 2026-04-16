# Supervisor-Worker

> 用一个主管节点负责任务拆解和分派，把具体执行交给多个专职 Worker，是多 Agent 系统里最常见也最容易落地的组织模式。

## 问题场景

当系统需要同时处理多种不同类型的子任务，但又不希望所有工具和 prompt 都塞进一个 Agent 里时，就需要一个上层调度者来做路由和协同。

典型场景：
- 一个 Agent 负责天气查询，另一个负责城市知识
- 一个 Agent 负责编码，另一个负责审阅
- 一个 Agent 负责研究，另一个负责汇总

## 解决方案

Supervisor 自己尽量不直接干活，而是做三件事：

1. 理解用户意图并拆分任务
2. 选择最合适的 Worker
3. 汇总 Worker 结果，决定是否继续派发或结束

Worker 则保持专职化：
- 各自有独立的 system prompt
- 各自绑定有限工具集
- 各自只对某类问题负责

这种分工让系统具备较清晰的职责边界。若底层框架支持流式 updates，还可以追踪任务经过了哪些节点、每个 Worker 返回了什么。

## 权衡取舍

- **优点**：路由清晰，角色边界明确，易于扩展更多 Worker，也方便并行化。
- **代价**：Supervisor 本身会成为系统瓶颈；如果调度策略差，容易出现错误分派或过度转发。
- **适用边界**：当任务之间需要高度共享上下文、持续双向协作时，单纯 Supervisor-Worker 可能不如更持续的团队协作机制。

## 关联页面

- [[concepts/multi-agent-architecture]]
- [[concepts/subagent]]
- [[concepts/agent-teams]]
- [[concepts/harness-engineering]]
- [[products/langgraph]]

## 参考来源

- 用户输入文章《LangGraph 和多 Agent 架构》（2026-04-16 收录）：`createSupervisor` + 两个 `createAgent` 子代理（天气 / 城市知识）的示例
