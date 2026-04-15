---
name: Model Context Protocol (MCP)
description: Anthropic 主导的开源协议，把 AI 接入外部服务的方式从"一个服务写一套对接"标准化成"即插即用"
type: concept
---

# Model Context Protocol（MCP）

> 让 AI 接入外部工具和数据源的统一协议。类比 USB-C：每个服务做一个标准接口，任何 AI 都能直接用。

## 解决的问题

协议出现前，AI 要连接一个外部服务（GitHub、Slack、数据库、CRM 等），需要专门写一套对接代码。N 个服务 = N 套对接 = N 个维护成本。

MCP 把这个 N×M 的胶水代码矩阵压缩成 N + M：服务方实现一次 MCP Server，AI 方实现一次 MCP Client，之后任意组合。

## 核心发起方与背书

- 由 [[products/claude-code]] 的母公司 Anthropic 发起并开源
- 2025 年底 Anthropic、OpenAI、Google **三家同时推动**作为行业标准——平时互相竞争的三家在这件事上合作，说明业内共识认为这是必须统一的基础设施

## 生态现状（2026 初）

常见服务均已提供 MCP Server：
- 代码与协作：GitHub、Jira、Slack
- 设计与文档：Figma、Notion
- 商业：Stripe
- 等等

多个 Claude Code、OpenClaw 及第三方 Agent 客户端原生支持 MCP。用户本机文件提供"最核心上下文"、MCP 把"剩下散落在云服务里的信息"补齐，构成一个 Agent 完整的上下文来源。

## 与其他协议的关系

- **MCP**：Agent 连接工具和数据（纵向：Agent ↔ 服务）
- **[[concepts/a2a-protocol]]**：Agent 之间互相通信（横向：Agent ↔ Agent）

两者结合，才拼出完整的 Agent 基础设施。

## 参考来源

- 官方文档：https://code.claude.com/docs/zh-CN/mcp
- 歸藏的AI工具箱《过了个年，AI 圈变天了？但没人告诉你为什么》（2026-02-25）

## 关联页面

- [[patterns/agent-four-layers-2026]]
- [[concepts/a2a-protocol]]
- [[concepts/claude-code-skills]]
- [[concepts/openclaw]]
