# Claude Code Skills

> Skills 层将特定类型任务的拆解方法固化为可复用工作流，使 Claude Code 遇到对应任务时能自动调用正确的处理模式。

## 核心要点

- Skills 解决的核心问题：Claude Code 遇到同类任务时，每次都需要重新描述应该如何拆解
- Skills 的本质：把"遇到这类任务怎么干"编码为可调用的程序化技能
- Skills 是 [[products/everything-claude-code]] 四层架构的第二层

## 详细说明

Skills 与 [[concepts/skill-system]]（Hermes Agent 中的技能系统）有相似的设计思想：都将工作流抽象为可复用的技能单元。

ECC 提供了 181 个预置 skill，覆盖常见的开发任务类型。当 Claude Code 识别到对应任务类型时，可以直接调用相应的 skill，而不是每次重新设计拆解路径。

Anthropic 官方的 Claude Agent SDK 也支持复用这套文件系统技能资产，但默认不会自动加载；需要通过 `settingSources` 显式启用，并在使用 `allowedTools` 白名单时加入 `Skill`。

用户输入文章《实战篇: Claude Code + superpowers + gstack 开发流程实录》提供了一个很有代表性的现实用法：把 skills 分成“方法论层”和“执行层”。其中 Superpowers 负责 brainstorm、plan、debug、review 等流程技能，gstack 负责浏览器、QA、ship、deploy 等执行技能。这个案例说明 Skills 不只是功能扩展点，也是一种给 Agent 划清职责边界的产品组织方式。

与此不同，用户输入文章《SkillForge：让企业级Agent Skills实现自主进化》展示的是企业场景里的另一条路线：Skill 不再只是 CLI 侧的工作流模块，而是可观测、可诊断、可迭代的能力包生命周期。

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
- [[products/claude-agent-sdk]] — 可通过 `settingSources` 复用 skills 的官方 SDK
- [[products/superpowers]] — 方法论型技能组合
- [[products/gstack]] — 执行型技能工具箱
- [[products/skillforge]] — 企业级 skill 自进化框架

## 参考来源

- 微信公众号：154K Star！Anthropic黑客松冠军的Claude Code配置大公开（2026-04-14）
- Anthropic 官方文档《Use Claude Code features in the SDK》（2026-04-16 查阅）
- 用户输入文章《实战篇: Claude Code + superpowers + gstack 开发流程实录，可直接复制使用，一篇文章讲清楚！》（2026-04-17 收录）
- 用户输入文章《SkillForge：让企业级Agent Skills实现自主进化》（2026-04-17 收录）
