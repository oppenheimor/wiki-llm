# Claude Code Configuration Layers

> 将 Claude Code 的使用经验拆分为 Rules/Skills/Hooks/Agents 四层可配置结构，使 AI 协作从高级对话框变为有记忆、可迭代、能协调的智能代理。

## 问题场景

传统 Claude Code 使用方式存在隐性成本：每次对话都需要重新解释项目上下文（代码规范、风格偏好、测试要求等）。这导致开发者陷入"每次都要说一遍"的重复劳动。

## 解决方案

ECC（[[products/everything-claude-code]]）提出的四层架构，将"每次都要说的话"编码为持久化的配置文件：

| 层级 | 功能 | 编码内容 |
|------|------|----------|
| Rules | 代码规范基准 | 项目规范、命名约定、测试要求 |
| Skills | 任务拆解方法 | 遇到某类任务时如何处理 |
| Hooks | 自动化后置动作 | 完成后自动干什么 |
| Agents | 任务委托对象 | 这种任务交给谁 |

## 分层思路的可复用性

文章作者建议：不必全部使用 181 个 skill，根据项目需求选择性的配置。重点是想清楚：
- 哪些行为应该是强制规则（Rules）
- 哪些应该是可调用的工作流（Skills）
- 哪些应该是自动触发的钩子（Hooks）

## 权衡取舍

- 学习成本：理解四层架构需要一定时间
- 配置量：181 个 skill 大部分可能与项目无关，需要筛选
- 维护成本：配置需要随项目演进更新

## 关联页面

- [[products/everything-claude-code]] — 该模式的具体实现（154K stars 仓库）
- [[concepts/claude-code-rules]] — Rules 层详解
- [[concepts/claude-code-skills]] — Skills 层详解
- [[concepts/claude-code-hooks]] — Hooks 层详解
- [[concepts/claude-code-agents]] — Agents 层详解

## 参考来源

- 微信公众号：154K Star！Anthropic黑客松冠军的Claude Code配置大公开（2026-04-14）