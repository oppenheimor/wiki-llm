# Constrained Decoding

> 在模型解码阶段主动限制“下一步允许输出哪些 token”，从而把自由文本生成收束为合法结构、有限选项或特定工具空间。

## 核心要点
- **它控制的不是“想法”，而是输出轨道**：模型内部依然会打分，但不被允许的 token 会在采样前被屏蔽掉。
- **Logit Mask 是核心手段**：把不合法 token 的 logit 压到极低或直接视为不可选，softmax 后这些 token 的概率趋近于 0。
- **结构化输出可靠性靠它兜底**：JSON、函数调用参数、枚举值、`yes/no` 这类格式约束，本质都可落到解码约束上。
- **它和 Prefill 常配合使用**：Prefill 锁起点，Constrained Decoding 锁后续合法空间，两者一起形成强约束。

## 详细说明
### 从 logits 到采样
模型每一步都会给词表中所有 token 一个原始分数（logits），经 softmax 变成概率分布，再按温度和采样策略选出一个 token。

Constrained Decoding 插手的位置就在“采样前”：
- 合法 token 保留
- 不合法 token 屏蔽

于是模型不是在“所有可能输出”里选，而是在“当前语法或规则允许的输出子集”里选。

### 为什么它对 Agent 特别关键
Agent 开发里，最脆弱的一环往往不是自然语言，而是“模型必须按协议输出”。例如：
- 工具调用参数必须是合法 JSON
- 路由命令必须落在限定枚举内
- 子 Agent 输出必须遵循固定 schema

如果只靠 prompt 提醒，模型偶尔就会跑偏；而解码约束提供了更硬的工程保证。

### 与 Structured Output 的关系
Structured Output 通常可以理解为“把输出格式约束前移到解码阶段”。模型看起来像是“会写标准 JSON”，但更准确地说，是系统在每一步只允许它生成当前语法下合法的 token。

## 上下文
该概念是理解函数调用、结构化输出和多 Agent 协议控制的底层抓手。没有这层，许多“为什么模型能稳定输出工具调用 JSON”的问题都只能停留在表面。

## 关联页面
- [[concepts/autoregressive-generation]]
- [[concepts/tokenization]]
- [[concepts/agent-loop]]
- [[concepts/harness-engineering]]
- [[products/claude-code-harness-analysis]]

## 参考文档
- 用户输入文章《做 Agent 开发，有些大模型本身的底层机制，你不得不了解》（2026-04-15 收录）
