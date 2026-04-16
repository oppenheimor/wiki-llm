# LangGraph

> LangChain 生态里的图编排框架，用显式状态图来组织 Agent、工具调用、分支、循环、中断与恢复。

## 核心能力

- **把 Agent 流程显式建模为图**：用 `StateGraph`、节点和边表达执行路径，不再局限于线性链式编排。
- **原生支持分支与循环**：条件路由和回边是一等能力，适合实现重试、分类分发、审阅回路等复杂控制流。
- **状态可持久化**：通过 checkpointer 保存图执行状态，可实现会话恢复、断点续跑与线程级上下文隔离。
- **支持人类中断与恢复**：`interrupt` + `Command({ resume })` 让图在关键节点暂停，等待人工确认后继续。
- **内置 Agent 常用节点**：`ToolNode`、`toolsCondition`、`createAgent` 等预构建能力把常见 Agent loop 直接封装成可复用图。

## 技术亮点

### 图编排替代线性编排
LangGraph 的重点不是“再包一层 Agent”，而是把原本隐含在 prompt 或 while 循环里的控制逻辑显式化。状态、分支、循环、失败重试、中断恢复都变成图结构的一部分，更适合复杂 Agent 产品调试和演进。

### State 是通信总线
节点之间不直接传参，而是通过共享 state 读写信息。`Annotation` 用来定义字段默认值与 reducer，决定新旧状态如何合并。这让单节点逻辑可以相对纯粹，图层专注在控制流。

### Checkpointer 让“图 = 可恢复程序”
当图状态可以按 `thread_id` 保存时，同一个工作流就不只是“一次性执行”，而是可暂停、可恢复、可多会话并行的程序。对于需要审批、长时任务或 coding agent 这类产品尤其关键。

### 多 Agent 只是图上的一种组织方式
Supervisor、Worker、工具节点、模型节点本质上都是图节点。多 Agent 不是脱离图编排的另一套东西，而是建立在图编排之上的更高层组织结构。

## 使用场景

- 构建带条件路由、重试、审批的复杂 Agent 工作流
- 为 coding agent、客服 agent、运营 agent 增加中断恢复能力
- 实现 `supervisor -> worker` 多 Agent 调度
- 把预构建 Agent loop 与自定义节点混合编排

## 关联页面

- [[concepts/agent-loop]]
- [[concepts/multi-agent-architecture]]
- [[patterns/supervisor-worker]]
- [[concepts/harness-engineering]]
- [[concepts/subagent]]
- [[concepts/agent-teams]]

## 参考来源

- 用户输入文章《LangGraph 和多 Agent 架构》（2026-04-16 收录）：`StateGraph`、条件分支、循环、`MemorySaver`、`interrupt`、`ToolNode`、`createAgent`、`createSupervisor` 示例
- LangChain 生态包：`@langchain/langgraph`、`@langchain/langgraph/prebuilt`、`@langchain/langgraph-supervisor`
