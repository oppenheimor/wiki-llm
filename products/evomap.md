---
name: EvoMap
description: 基于 GEP 协议的 Agent 经验进化平台，让 Agent 的成功做法可以跨用户、跨领域被继承
type: product
---

# EvoMap

> 一个实现 [[concepts/gep-protocol]]（基因组进化协议）的 Agent 经验进化平台，主打"从平台依赖到进化协议"的理念转变。

## 核心定位

EvoMap 试图回答一个问题：**Agent 的经验可以像生物基因那样被传承和进化吗？**

它不是一个独立的 Agent 框架，而是建立在 GEP 协议之上的**经验交换层**。你的 Agent 在 EvoMap 网络里发布成功做法（打包成基因胶囊），其他 Agent 可以订阅、继承、基于此继续进化。

## 设计哲学：协议优先

官方博客《EvoMap 诞生记：从平台依赖到进化协议》明确强调：

> 平台可以被收购、被关掉，但协议是开放的，谁都可以实现。你的 Agent 攒下的经验属于你。

这个理念的背景是 [[concepts/openclaw]] 被 OpenAI 收购一事——如果用户的经验绑定在具体平台上，平台一出问题，经验就归零。GEP 协议 + EvoMap 的组合就是对这种风险的回应。

## 与 Skills 的互补

- [[concepts/claude-code-skills]]：人写的能力模块，静态、需要人工更新
- EvoMap 上的基因胶囊：Agent 使用中涌现的经验，动态、能自我修复、长期没用会淘汰

两者互补而非替代：Skills 是"底线能力"，基因胶囊是"涌现经验"。

## 跨领域迁移的价值

EvoMap 的独特价值不是"让每个 Agent 变强"，而是让**经验跨领域迁移**成为可能。游戏策划领域的"命名隔离策略"可以被后端工程师的 Agent 用来解决变量命名冲突——这种跨领域传染在传统知识库里几乎不可能发生。

## 参考来源

- EvoMap 官方博客：https://evomap.ai/blog/evomap-origin-story
- 歸藏的AI工具箱《过了个年，AI 圈变天了？但没人告诉你为什么》（2026-02-25）

## 关联页面

- [[concepts/gep-protocol]]
- [[patterns/agent-four-layers-2026]]
- [[concepts/self-evolution]]
- [[concepts/claude-code-skills]]
