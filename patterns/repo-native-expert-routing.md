# Repo-Native Expert Routing

> 面向复杂代码库的多 Agent 系统，不应依赖一个巨大的总说明文档或模糊猜测式路由，而应把 repo 内文档作为唯一事实源，并用结构化路由表把问题映射到对应专家 Agent。

## 问题场景
当一个 Agent 需要覆盖文档、代码、cookbook、部署约束、模型配置等多个子域时，最直觉的做法通常是把所有知识塞进一个大 prompt 或一份巨型 `AGENTS.md`。这种做法短期看简单，长期却几乎必然腐烂：
- 信息越来越多，注意力越来越分散
- 文档过时后会主动误导 Agent
- 路由依赖 Manager 猜测，容易漏掉真正相关的专家

## 解决方案
将系统拆成多个子域 expert，并遵循两条原则：
- **Repo 是唯一事实源**：专家知识优先来自仓库内维护的 markdown 与代码，而不是外部临时说明或口头知识。
- **结构化路由，不靠猜**：维护一份 Expert Routing Table，明确什么问题应激活哪些 expert，可同时激活多个相关专家。

这样做的效果是，知识维护与问题路由都前移到结构化资产层，而不是每次请求时让上层 Agent 重新猜一遍。

## 权衡取舍
这个模式需要前期投入去维护 repo 内文档质量和路由表索引，也意味着必须持续清理过时知识。它把复杂度从“运行时临场猜测”转移到了“离线知识组织”，但换来的是更稳定的多 Agent 行为和更低的上下文噪音。

## 关联页面
- [[concepts/multi-agent-architecture]]
- [[concepts/subagent]]
- [[patterns/supervisor-worker]]
- [[concepts/harness-engineering]]

## 参考来源
- 用户提供截图文章《Agent 时代，工程师最值钱的能力是说“不”》（2026-04-17 收录）
