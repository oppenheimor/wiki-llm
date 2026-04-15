# Agent Loop

> Agent 的最小运行内核：让模型在一个持续循环里自主决定“下一步做什么”，直到任务完成、失败或被外部打断。

## 核心要点
- **本质是控制权转移**：从 ChatBot 的“人问一句答一句”，转向 Agent 的“模型自己掌控下一步行动”。
- **最小形式就是 `while (true)`**：每轮先让模型决定是否调用工具，再执行工具，把结果塞回上下文，继续下一轮。
- **核心闭环是 Think / Act / Observe**：想一步、做一步、看一步；其中 Observe 不是附属品，而是后续决策的前提。
- **生产级复杂度主要来自异常处理**：退出条件、上下文压缩、权限审批、流式中断、工具失败恢复，远比“主循环”本身复杂。
- **Agent 产品的差异往往不在模型本身，而在 Loop 外围的 Harness**：工具系统、上下文工程、权限边界、状态管理共同决定“能不能干活”。

## 详细说明
### 最小可运行形态
一个最小 Agent Loop 可以抽象成：

```ts
while (true) {
  const response = await llm.chat(messages)
  if (response.toolCalls.length === 0) break

  for (const call of response.toolCalls) {
    const result = await executeTool(call)
    messages.push(result)
  }
}
```

这个结构看起来只有十来行，但它已经完成了 Agent 的核心跃迁：模型不再只是回答问题，而是在循环中持续决定行动。

### 为什么是开放式循环
任务复杂度不可预先枚举。一次“帮我把 Express 迁移到 Hono”可能 5 轮完成，也可能因为测试失败、中间件兼容性和类型报错跑 30 轮。因此 Agent 不能预设固定步数，只能采用“做到结束为止”的开放式循环，并额外加最大轮次等保险丝。

### Observe 是最容易被低估的一步
很多“伪 Agent”只实现了 tool calling，却没有认真设计 observation。若工具执行结果没有被结构化地塞回上下文，模型下一轮只能盲猜。Agent 之所以能自我修正，关键不在“会调用工具”，而在“看得到工具返回了什么”。

### 从最小 Loop 到工业级 Harness
真实产品里的 Agent Loop 不只是一个 while 循环。它通常还要处理：
- 上下文压缩与窗口保护
- 流式输出与边生成边执行
- 并发与串行工具调度
- 多种退出原因与恢复路径
- 权限审批、危险操作拦截、失败重试
- 回合状态、挂起任务、压缩历史、调试轨迹

因此，Agent Loop 更适合被理解成 Harness 的调度核心，而不是全部系统本身。

## 上下文
该概念是理解 ChatBot / Copilot / Agent 三种交互形态差异的最小抓手，也是理解 [[concepts/harness-engineering]]、[[products/learn-claude-code]]、[[products/claude-code-harness-analysis]] 的入口概念。

## 关联页面
- [[concepts/react-pattern]]
- [[concepts/harness-engineering]]
- [[concepts/mcp]]
- [[concepts/subagent]]
- [[products/learn-claude-code]]
- [[products/claude-code-harness-analysis]]
- [[comparisons/chatbot-vs-copilot-vs-agent]]

## 参考文档
- 用户输入文章《从 ChatBot 到 Agent：一个 while 循环，凭什么让 AI 从"能聊天"变成"能干活"？》（约 21 分钟，2026-04-15 收录）
- Anthropic《Building Effective Agents》：Workflow 与 Agent 的区分（文中引用）
