# Claude Code Skills

> Skills 层将特定类型任务的拆解方法固化为可复用工作流，使 Claude Code 遇到对应任务时能自动调用正确的处理模式。

## 核心要点

- Skills 解决的核心问题：Claude Code 遇到同类任务时，每次都需要重新描述应该如何拆解
- Skills 的本质：把"遇到这类任务怎么干"编码为可调用的程序化技能
- Skills 是 [[products/everything-claude-code]] 四层架构的第二层

## 详细说明

Skills 与 [[concepts/skill-system]]（Hermes Agent 中的技能系统）有相似的设计思想：都将工作流抽象为可复用的技能单元。

ECC 提供了 181 个预置 skill，覆盖常见的开发任务类型。当 Claude Code 识别到对应任务类型时，可以直接调用相应的 skill，而不是每次重新设计拆解路径。

## 与 Hermes Agent Skill System 的关联

[[concepts/skill-system]] 是 Hermes Agent 的核心能力，将工作流自动抽象为可复用技能。ECC Skills 与之一脉相承，但专注于 Claude Code 场景。

## 在四层架构中的位置

- **Rules**：规范层 — 代码标准是什么
- **Skills**：技能层 — 任务如何拆解（本文档）
- **Hooks**：自动化层 — 完成后自动干什么
- **Agents**：委托层 — 任务交给谁

## 关联页面

- [[products/everything-claude-code]] — Skills 所属的四层配置体系
- [[concepts/skill-system]] — 类似的技能抽象思路（Hermes Agent）
- [[patterns/claude-code-config-layers]] — 分层配置的整体思路

## 参考来源

- 微信公众号：154K Star！Anthropic黑客松冠军的Claude Code配置大公开（2026-04-14）
