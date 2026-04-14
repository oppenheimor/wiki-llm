# Claude Code Agents

> Agents 层将特定类型任务直接委托给对应的 sub-agent，实现任务分流，让专业工具处理专业问题。

## 核心要点

- Agents 层解决的核心问题：Claude Code 遇到需要专项处理的任务时，全部由主 agent 承担效率低下
- Agents 的本质：把"这种任务直接交给谁"编码为配置
- Agents 是 [[products/everything-claude-code]] 四层架构的委托层

## 详细说明

[[products/everything-claude-code]] 提供了 47 个预置 sub-agent，覆盖不同开发场景。当 Claude Code 识别到适合专项处理的任务时，直接委托给对应的 sub-agent，而不是让主 agent 全程处理。

这种模式体现了专业分工的思想：每个 sub-agent 都有其专注的领域，协同工作比单一 agent 全能处理效率更高。

## 与 [[concepts/hermes-agent]] 的关联

[[concepts/hermes-agent]] 同样采用 Agent 协调架构，ECC 的 Agents 层与其有相似的设计思想——通过多 Agent 协作分担不同类型的任务。

## 在四层架构中的位置

- **Rules**：规范层 — 代码标准是什么
- **Skills**：技能层 — 任务如何拆解
- **Hooks**：自动化层 — 完成后自动干什么
- **Agents**：委托层 — 这种任务交给谁（本文档）

## 关联页面

- [[products/everything-claude-code]] — Agents 所属的四层配置体系（包含 47 个 sub-agent）
- [[concepts/hermes-agent]] — 类似的 Agent 协调架构
- [[patterns/claude-code-config-layers]] — 分层配置的整体思路

## 参考来源

- 微信公众号：154K Star！Anthropic黑客松冠军的Claude Code配置大公开（2026-04-14）
