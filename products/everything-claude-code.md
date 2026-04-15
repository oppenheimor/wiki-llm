# Everything Claude Code

> 154K stars 的 Claude Code 配置仓库，通过 Rules/Skills/Hooks/Agents 四层架构将 AI 协作经验编码为可复用配置。

## 核心能力

- **47 个 sub-agent**：预置的任务委托单元，覆盖不同开发场景
- **181 个 skill**：可复用的任务拆解工作流
- **79 个命令**：快捷操作入口
- **黑客马拉松冠军**：Anthropic 官方 Hackathon 大奖作品

## 解决的问题

传统 Claude Code 使用方式的隐性成本：每次对话都需要重新解释上下文（项目规范、代码风格、测试要求、包管理器偏好等）。

ECC 的核心逻辑：把这些每次都要说的话变成 Claude Code 的默认行为，而不是每次重新输入。

## 四层架构

### Rules（规则层）
负责定义项目的代码规范是什么，作为 Claude Code 的默认行为基准。

### Skills（技能层）
负责遇到特定类型任务时如何拆解，将工作流固化为可调用程序。

### Hooks（钩子层）
负责每次做完某件事之后自动干什么，是最容易产生质变的自动化机制。

### Agents（代理层）
负责将特定类型任务直接委托给对应的 sub-agent，实现任务分流。

## 关键 Hook 详解

### memory-persistence hook
会话开始时自动加载上下文，结束时自动保存状态。下次打开项目时 Claude Code 知道你上次做到哪了、有哪些未解决的问题，不需要重新介绍背景。

### suggest-compact hook
当上下文窗口快满时主动提醒做精简，避免 token 被耗尽时才发现。

## AgentShield

内置的安全扫描工具，1282 项测试，102 条静态分析规则。检查 CLAUDE.md、MCP 配置、hooks 中是否存在：
- 密钥泄露风险
- 权限配置问题
- 注入风险

使用方式：
```bash
npx ecc-agentshield scan
```

## 与 Hermes Agent 的对照

文章作者认为 Hermes Agent 的价值在于把"怎么干"变成了可复用的结构。ECC 的价值类似——把优秀开发者的 Claude Code 使用经验编码成了可被他人直接加载的配置。

两者共同体现的思路：[[patterns/claude-code-config-layers]]。

## 关联页面

- [[concepts/hermes-agent]] — 文中对比参照的 Agent 框架
- [[patterns/claude-code-config-layers]] — ECC 背后的分层配置思路
- [[products/agent-shield]] — ECC 内置的安全扫描工具
- [[concepts/claude-code-routines]] — 云端自动化运行功能
- [[concepts/harness-engineering]] — 四层配置体系是 Harness 工程的具体实践形式
- [[products/claude-code-harness-analysis]] — Claude Code 源码层面的完整 Harness 架构分析（1,900 文件、512K 行 TypeScript）

## 参考来源

- 微信公众号：154K Star！Anthropic黑客松冠军的Claude Code配置大公开（2026-04-14）
- 仓库地址：github.com/affaan-m/everything-claude-code
