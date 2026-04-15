# Tokenization

> 把人类可读的文本切分成模型可处理的离散 token 序列的过程；上下文窗口、计费、缓存命中和压缩触发，最终都建立在这层离散化之上。

## 核心要点
- **模型不直接理解“文字”**：任何中文、英文、代码、标点都会先被编码成 token ID 序列。
- **Token 是 Agent 工程的计量单位**：上下文窗口、输入输出成本、压缩阈值、工具描述开销都按 token 计算。
- **中文通常比英文更“费 token”**：同等语义下，中文在很多 tokenizer 上的 token 消耗高于英文，这会放大长任务里的成本与窗口压力。
- **分词策略会影响工程判断**：系统提示词写法、工具 schema 长度、日志格式甚至语言选择，都会受 tokenization 影响。

## 详细说明
### 为什么需要 token
LLM 的输入输出本质上都是数字序列。Tokenization 把连续文本转换成可被神经网络处理的离散符号，使“生成文字”这个任务落到“预测下一个 token 编号”上。

### BPE 与“中文更碎”
许多主流模型基于 BPE（Byte Pair Encoding）或其变体。它的思路不是先理解词义，而是从频繁共现的字节或字符组合里逐步合并高频片段。

这带来一个常见现象：
- 英文里常见单词和词片更容易被合并成单个 token
- 中文由于字符集大、UTF-8 编码通常占更多字节，很多常见表达仍会被拆成更细的片段

因此，在很多模型上，中文 prompt、中文工具返回和中文日志的 token 消耗会系统性高于英文。

### 对 Agent 的实际影响
在一轮普通问答里，这点差异不一定显著；但在 Agent 场景中，system prompt、工具定义、对话历史、工具结果会跨多轮累计，token 预算会被放大消耗。于是：
- 压缩更早触发
- 成本估算更容易低估
- 工具 schema 和长日志更容易挤占有效工作上下文

这也是为什么很多 Agent 系统会对 token 估算额外留安全边距。

## 上下文
该概念是理解 [[concepts/agent-loop]]、[[concepts/kv-cache]]、[[concepts/constrained-decoding]] 和上下文工程的底层入口。没有 tokenization，后续关于缓存、流式生成、结构化输出的讨论都会悬空。

## 关联页面
- [[concepts/autoregressive-generation]]
- [[concepts/kv-cache]]
- [[concepts/constrained-decoding]]
- [[concepts/agent-loop]]
- [[concepts/harness-engineering]]
- [[products/claude-code-harness-analysis]]

## 参考文档
- 用户输入文章《做 Agent 开发，有些大模型本身的底层机制，你不得不了解》（约 23 分钟，2026-04-15 收录）
