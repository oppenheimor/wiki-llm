---
name: Agent Teams（多智能体协同）
description: Anthropic 推出的让一个主 Agent 编排多个持续存在的团队成员并行工作的机制
type: concept
---

# Agent Teams（多智能体协同）

> Anthropic 在 Claude Code 上推出的多智能体协作机制。一个主 Agent（Team Lead）创建和管理多个持续存在的团队成员（Teammate），每个成员有独立的专长、工具集和上下文窗口，在各自的空间里并行工作、互不干扰。

## 与 SubAgent 的区别

| | [[concepts/subagent]] | Agent Teams |
|---|---|---|
| 生命周期 | 临时、完成即消失 | 持续存在的团队成员 |
| 关系 | 主 Agent 单向调用 | Team Lead ↔ Teammate 双向协调 |
| 通信 | 子 Agent 只返回摘要 | 成员之间可以互相沟通 |
| 用途 | 搜索压缩、上下文保护 | 长期复杂项目的多角色协作 |

SubAgent 解决"一个 Agent 怎么高效处理复杂任务"，Agent Teams 解决"怎么让多个 Agent 像一个团队一样持续协作"。

## 典型使用方式

用户对主 Agent 说"帮我做一个电商网站"，主 Agent 自己拆任务：
- 一个成员写后端接口
- 一个做前端页面
- 一个写数据库
- 一个跑测试

成员卡住了向主 Agent 汇报，主 Agent 来协调。用户是老板，主 Agent 是项目经理，团队成员是各岗位的员工——用户只需要跟项目经理沟通。

## 压力测试：16 个 Agent 写 C 编译器

Anthropic 安全团队做过一个压力测试：
- **配置**：16 个 [[products/claude-opus-4-6]] 实例组成一个 Agent Team
- **任务**：在没有人类干预的情况下，从零开始用 Rust 写一个能编译 Linux 内核的 C 语言编译器
- **规模**：约 2 万美元、近 2000 个会话周期、10 万行代码产出

## 并发冲突解决：用 Git 锁认领任务

16 个 Agent 同时写代码怎么不打架？他们用了一个很聪明的办法——通过 Git 的文件锁机制来"认领"任务：
- 每个 Agent 开工前在仓库里放一个锁文件，声明"这块我来"
- Git 天然的防冲突机制保证不会有两个 Agent 同时改同一个文件
- 干完自己提交代码、解锁、去认领下一个任务

这是把"成熟的分布式系统思路（分布式锁）"迁移到 Agent 协作场景的一个经典案例。

## 配合 Git Worktree 的"平行宇宙"

Agent Teams 配合 Git Worktree 可以做到一件人类团队做不到的事：同时探索多个方案。

- 传统方式：先试 A 方案，不行再试 B，再不行试 C（串行，1~2 周）
- Agent Teams + Worktree：创建 3 个独立工作空间，每个放一个 Team 按 A/B/C 方案同时开发（并行，时间 1/3，探索量 ×3）

本质是在用**并行计算的方式做决策**。

## 参考来源

- 官方文档：https://code.claude.com/docs/zh-CN/agent-teams
- 歸藏的AI工具箱《过了个年，AI 圈变天了？但没人告诉你为什么》（2026-02-25）

## 关联页面

- [[patterns/agent-four-layers-2026]]
- [[concepts/subagent]]
- [[concepts/parallel-subagent-debugging]]
- [[concepts/a2a-protocol]]
- [[products/claude-code]]
