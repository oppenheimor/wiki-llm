# KV Cache

> Transformer 在生成过程中缓存已计算过的 Key / Value 表示，以避免每生成一个新 token 都从头重算全部历史上下文。

## 核心要点
- **缓存的是 Attention 里的 K 和 V，不是最终文本**：它复用的是“已经算过的中间表示”，而不是模型回答本身。
- **前缀稳定性决定复用率**：只要前缀完全一致，后续轮次就能复用前面大段历史；前缀一变，缓存会大面积失效。
- **它直接影响延迟与成本**：长上下文任务里，KV Cache 命中率常常是最关键的生产指标之一。
- **它解释了很多 Agent 设计约束**：为什么系统提示词尽量稳定、为什么工具定义别乱抖、为什么新增内容最好只往后追加。

## 详细说明
### Attention 为什么需要缓存
生成新 token 时，当前 token 会对历史上下文做 attention 计算。历史里每个 token 都携带自己的 Key 与 Value；如果每一轮都重新计算全部历史表示，长上下文成本会迅速爆炸。

KV Cache 的优化思路很朴素：历史部分如果没变，就直接复用之前算好的 Key / Value，只计算这次新增的 token。

### 前缀匹配是生死线
KV Cache 的复用依赖“前缀完全相同”。这意味着：
- 在末尾追加一条新用户消息，前面历史通常可复用
- 但如果在 system prompt 开头加一个动态时间戳，往往会让后面整段前缀失配，缓存命中率直接归零

这也是 Agent 系统里常见的一条工程铁律：**稳定的内容放前面，变化的内容尽量追加到后面。**

### 与上下文工程的关系
KV Cache 不能解决“长上下文注意力稀释”的问题，只解决“别重复算一样的历史”这个问题。它和上下文压缩是互补关系：
- 缓存解决算力与成本浪费
- 压缩解决注意力预算与上下文腐烂

### 为什么很多 Agent 天生就把缓存打烂
用户提供截图文章《Agent 时代，工程师最值钱的能力是说“不”》指出，许多 Agent 框架虽然表面上支持长 session，但请求构造方式并没有围绕 cache 复用设计。常见问题包括：多轮低价值 tool call 反复携带巨型上下文、resume 导致前缀失配、会话状态在每轮请求中被整段重放。结果是推理引擎一侧精心设计的 prefix cache 机制，被上层编排直接打穿。

这也提醒我们，KV Cache 优化不是单边问题。只优化模型或推理引擎不够，Agent 框架本身是否 cache-aware，往往才是长 session 成本的真正分水岭。

## 上下文
该概念是理解 Prompt Caching、上下文压缩和 Agent 成本优化的关键中间层。它解释了为什么同样一个 Agent，提示词布局的小改动也可能在价格和延迟上造成数量级差异。

## 关联页面
- [[concepts/tokenization]]
- [[concepts/agent-loop]]
- [[concepts/harness-engineering]]
- [[concepts/autoregressive-generation]]
- [[concepts/token-efficiency]]
- [[concepts/engineering-sense]]
- [[products/claude-code-harness-analysis]]

## 参考文档
- 用户输入文章《做 Agent 开发，有些大模型本身的底层机制，你不得不了解》（2026-04-15 收录）
- 用户提供截图文章《Agent 时代，工程师最值钱的能力是说“不”》（2026-04-17 收录）
