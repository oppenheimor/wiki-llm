# ReAct Pattern

> 一种把 LLM 行为拆成 Reasoning、Acting、Observation 三个交替阶段的 Agent 基础范式，强调“边想、边做、边根据结果修正”。

## 核心要点
- **ReAct 不是只会“想”和“做”**：真正闭环依赖 Observation，把工具结果重新纳入上下文。
- **它是大多数 Agent 产品的默认认知骨架**：模型通过一轮轮推理与行动逐步逼近目标，而非一次性规划到终点。
- **其工程价值在于自我修正**：模型能在读到报错、测试失败、文件现状后调整下一步动作。
- **ReAct 与 Agent Loop 是两层概念**：ReAct 描述认知节奏，[[concepts/agent-loop]] 描述执行载体。

## 详细说明
### 三段式闭环
ReAct 可概括为：
- **Reasoning**：模型判断当前状态，决定下一步最合适的动作
- **Acting**：调用工具或执行外部操作
- **Observation**：把工具返回结果、系统状态变化、错误信息重新喂给模型

如果缺少 Observation，模型就只是“连续猜测”；如果只有 Reasoning 没有 Acting，模型就退化为纸上谈兵。

### 为什么它适合开放世界任务
代码修改、网页操作、搜索资料、调接口都属于“环境会反过来影响后续决策”的问题。ReAct 的优势在于它不要求模型一开始就规划出完整路径，而是允许路径随着观察结果不断修正。

### 在 Coding Agent 中的典型表现
一个表现良好的 Coding Agent 往往会出现以下模式：
- 先读文件再决定怎么改
- 修改后自查遗漏的 import、类型或依赖
- 主动运行测试或命令验证结果
- 根据错误日志回退并修正方案

这些行为并不是硬编码脚本流程，而是 ReAct 闭环在工程环境中的自然涌现。

## 上下文
该概念常作为 Agent 入门时解释“为什么模型能多轮自主干活”的最小理论框架，和 [[concepts/agent-loop]]、[[concepts/harness-engineering]] 一起构成 Agent 工程的基础词汇。

## 关联页面
- [[concepts/agent-loop]]
- [[concepts/harness-engineering]]
- [[products/learn-claude-code]]
- [[comparisons/chatbot-vs-copilot-vs-agent]]

## 参考文档
- 用户输入文章《从 ChatBot 到 Agent：一个 while 循环，凭什么让 AI 从"能聊天"变成"能干活"？》（2026-04-15 收录）
- ReAct 论文概念在文中作为 Agent 标准范式被引用
