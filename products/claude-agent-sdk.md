# Claude Agent SDK

> Anthropic 提供的官方 Agent 开发 SDK，把 Claude Code 的工具、agent loop 与上下文管理能力以 Python 和 TypeScript 库的形式开放给开发者。

## 核心能力

- **Claude Code 同源执行内核**：SDK 直接复用 Claude Code 的工具系统、agent loop 和上下文管理，不需要开发者自己实现 tool loop。
- **内置工具可直接开工**：开箱可用 `Read`、`Edit`、`Write`、`Bash`、`Glob`、`Grep`、`WebSearch`、`WebFetch`、`Monitor`、`AskUserQuestion` 等工具。
- **支持多种 Agent 扩展原语**：可配置 hooks、subagents、sessions、MCP、自定义工具、结构化输出与权限控制。
- **可按需加载 Claude Code 文件系统能力**：通过 `settingSources` 显式接入 `CLAUDE.md`、skills、hooks、slash commands 等工程内配置。
- **支持 Python 与 TypeScript**：分别以 `claude-agent-sdk` 与 `@anthropic-ai/claude-agent-sdk` 发布，适合脚本、服务端和产品化集成。

## 技术亮点

### 它卖的不是“调一次模型”，而是“把 Claude Code 当成可编程运行时”
与需要开发者自己实现工具执行循环的 Client SDK 不同，Claude Agent SDK 直接把 Claude Code 那套 Agent Runtime 暴露为库接口。你写的是 prompt、权限与宿主集成，而不是一堆 `while tool_use -> execute -> append result` 胶水代码。

### 默认隔离，按需继承 Claude Code 能力
自 v0.1.0 起，SDK 默认不再自动继承 Claude Code 的 system prompt 和文件系统设置，而是以更隔离的最小环境启动。需要时再显式启用 `settingSources` 或 `systemPrompt preset`，这让 SDK 更适合嵌入生产系统，而不是偷偷带上 CLI 侧假设。

### Claude Code 配置资产可复用到 SDK
项目里的 `CLAUDE.md`、`.claude/skills/*/SKILL.md`、hooks、slash commands 等文件系统能力，可以通过 `settingSources` 接进 SDK Agent。这意味着同一套项目知识和工作流，可以同时服务交互式 Claude Code 与程序化 Agent。

### Agent 能力是组合件，不是单点 API
官方文档把 hooks、MCP、subagents、sessions、permissions、skills、structured outputs、tool search 等都放在同一个 SDK 体系下，说明它的定位不是“一个会调工具的聊天封装”，而是完整的 Agent Product SDK。

## 使用场景

- 把 Claude Code 的能力嵌入 CI/CD、后台服务或内部开发平台
- 为现有产品添加能读文件、跑命令、调 MCP、做代码修改的 Agent 能力
- 需要显式控制 permissions、hooks、sessions 的生产级 Agent 应用
- 希望复用现有 `CLAUDE.md`、skills、hooks 资产，而不是为 SDK 再维护一套平行配置

## 与相关工具的关系

- **相对 Anthropic Client SDK**：Client SDK 只给模型 API；Claude Agent SDK 直接内建工具执行与 Agent loop。
- **相对 Claude Code CLI**：两者能力底座相同，但 CLI 面向交互式开发，SDK 面向自动化、集成和产品化嵌入。
- **相对 Claude Managed Agents**：Agent SDK 仍由开发者自己决定运行环境与基础设施边界；Managed Agents 则把环境、会话和事件流一起托管掉，更接近 hosted harness。
- **相对 Claude Code SDK**：Claude Code SDK 是旧名称；该 SDK 已重命名为 Claude Agent SDK，并调整了默认 system prompt 与 settings 加载行为。

## 关联页面

- [[concepts/agent-loop]] — SDK 暴露的核心运行内核
- [[concepts/tool-execution-pipeline]] — SDK 将工具执行、权限与 Hook 等联锁能力开放为可编程运行时
- [[concepts/subagent]] — SDK 支持把子任务委托给专门 subagent
- [[concepts/mcp]] — SDK 可接入外部 MCP Server 扩展能力边界
- [[concepts/claude-code-skills]] — 可通过 `settingSources` 复用 skills
- [[products/learn-claude-code]] — 以 Claude Code Harness 为教学对象的 0→1 教程
- [[products/everything-claude-code]] — 文件系统配置资产可迁移到 SDK
- [[concepts/claude-to-im]] — 该工具集的开发者 SDK 场景直接依赖 Agent SDK
- [[products/claude-managed-agents]] — Anthropic 托管式 hosted harness 形态
- [[concepts/prompt-cache]] — SDK 同样受稳定前缀与缓存命中约束

## 参考来源

- 官方文档（overview）：https://code.claude.com/docs/en/agent-sdk/overview
- 官方文档（migration-guide）：https://code.claude.com/docs/en/agent-sdk/migration-guide
- 官方文档（claude-code-features）：https://code.claude.com/docs/en/agent-sdk/claude-code-features
- 官方文档索引（llms.txt）：https://code.claude.com/docs/llms.txt
- 用户输入文章《Anthropic 官方 Agent Harness 平台：Claude Managed Agents 完整指南》（2026-04-17 收录）
