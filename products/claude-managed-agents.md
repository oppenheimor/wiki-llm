# Claude Managed Agents

> Anthropic 提供的托管式云端 Agent 运行平台，把环境、工具、会话与事件流编排成可直接使用的 hosted harness。

## 核心能力
- **托管运行时**：开发者不必自己搭建沙箱、状态管理、错误恢复和工具执行循环。
- **四个核心原语**：以 Agent、Environment、Session、Events 组织整个运行模型。
- **内置工具与扩展能力**：可使用默认工具集，也可接自定义工具或 MCP 服务。
- **持续会话**：Session 以独立容器承载状态、文件系统、进程和网络，支持多轮连续工作。
- **多智能体预览**：在主 Agent 之上提供协调器与工作者式编排雏形。

## 技术亮点
### 它是 Harness as a Service 的典型产品化形态
如果 Claude Agent SDK 是“把 Claude Code Runtime 作为库开放”，Claude Managed Agents 更像“把 Harness 作为平台开放”。开发者定义任务与约束，底层执行环境由平台托管。

### 运行模板被抽象为 Environment
Environment 负责预装依赖、控制网络、挂载仓库等，使“运行条件”成为显式配置，而不是每次会话里手工准备。这让托管式 Agent 更接近可复用的基础设施，而不只是一次性 API 调用。

## 使用场景
- PR 审查、代码生成、文档处理、后端自动化等长运行任务
- 不想自己维护 Agent Runtime 基础设施的团队
- 需要用托管会话承载持续状态和事件流交互的产品化 Agent

## 关联页面
- [[concepts/harness-engineering]]
- [[concepts/agent-loop]]
- [[concepts/mcp]]
- [[concepts/multi-agent-architecture]]
- [[concepts/prompt-cache]]
- [[products/claude-agent-sdk]]

## 参考来源
- 用户输入文章《Anthropic 官方 Agent Harness 平台：Claude Managed Agents 完整指南》（2026-04-17 收录）
