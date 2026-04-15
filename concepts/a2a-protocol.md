---
name: Agent-to-Agent (A2A) 协议
description: Google 联合 50+ 企业推出的跨厂商 Agent 通信协议，让不同生态的 Agent 能互相协作
type: concept
---

# A2A（Agent-to-Agent）协议

> 让不同厂商、不同模型的 Agent 之间能互相沟通和协作的开放协议。与 [[concepts/mcp]] 互补——MCP 解决"Agent ↔ 工具"，A2A 解决"Agent ↔ Agent"。

## 定位

Agent 基础设施的横向通信层：
- **MCP**（Anthropic 主导）：纵向，Agent 连工具/数据
- **A2A**（Google 主导 + 50 多家企业）：横向，Agent 之间的跨生态协作

意味着你的 Claude Agent 可以跟别人的 GPT Agent 协同工作，而不再局限在单一生态内。

## 为什么需要它

单个厂商内部已经解决了 Multi-Agent 协作（如 [[concepts/agent-teams]]），但真实世界里的 Agent 会来自不同公司、跑在不同模型上。没有统一协议，跨厂商的 Agent 之间没法交换任务、共享状态、互相调度。

A2A 的目标就是把"跨生态协作"变成可能，拒绝让 Agent 世界退化成一堆互不兼容的围墙花园。

## 产业意义

和 MCP 一样，A2A 的存在本身就是一个信号：行业认识到 Agent 不能被某家公司垄断，基础设施必须开放。这也呼应了 [[concepts/gep-protocol]] "协议不是平台，协议归用户"的理念。

## 参考来源

- 歸藏的AI工具箱《过了个年，AI 圈变天了？但没人告诉你为什么》（2026-02-25）

## 关联页面

- [[patterns/agent-four-layers-2026]]
- [[concepts/mcp]]
- [[concepts/agent-teams]]
- [[concepts/gep-protocol]]
