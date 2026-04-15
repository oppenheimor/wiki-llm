# Autoregressive Generation

> 大模型生成文本的基本方式：每次只生成一个新 token，再把它接回上下文，继续预测下一个 token。

## 核心要点
- **模型不是“先想完再说”**：它是边生成、边基于已生成内容继续决策。
- **流式响应是机制自然外显**：界面上的“打字机效果”不是装饰，而是自回归生成过程的直接投影。
- **工具调用必须等结构完整**：函数调用或 JSON 参数会以 token 碎片流出，执行器需要攒到语法闭合后才能真正解析。
- **Prefill 能改变行为轨道**：提前写入 assistant 前缀，相当于替模型锁定起跑方向，后续生成只能顺着往下走。

## 详细说明
### 一次只决定一个 token
给定当前上下文，模型会先为词表里的所有候选 token 打分，再选出当前步要输出的一个 token。这个新 token 被追加到上下文后，模型再进入下一步。循环往复，直到生成结束标记或被外部停止。

### 为什么它对 Agent 特别重要
对 Agent 来说，自回归生成不是理论细节，而是产品行为本身的根：
- **流式 UI**：生成到哪展示到哪
- **流式工具执行**：工具参数的 token 片段逐步到达，执行器要判断何时已可安全解析
- **行为引导**：通过 response prefill 或结构前缀，把模型推进特定输出轨道

### Prefill 与工具约束
如果提前把 assistant 输出前缀写成某段固定结构，比如某个工具名的前缀，模型无法“回头修改已经说过的话”，只能在这个前缀下继续补全。这种技巧常用于阶段性限制工具空间，成本低于删改整套工具定义。

## 上下文
该概念是 [[concepts/agent-loop]] 的时间维度展开：Agent Loop 描述“回合之间怎么转”，Autoregressive Generation 描述“单次响应内部怎么一 token 一 token 地往前滚动”。

## 关联页面
- [[concepts/tokenization]]
- [[concepts/constrained-decoding]]
- [[concepts/agent-loop]]
- [[concepts/react-pattern]]
- [[products/claude-code-harness-analysis]]

## 参考文档
- 用户输入文章《做 Agent 开发，有些大模型本身的底层机制，你不得不了解》（2026-04-15 收录）
