# 多 Agent 架构

> 把原本塞进单个 Agent 的职责拆到多个专职 Agent 中，让每个 Agent 只携带必要 prompt、工具与上下文，再由上层协调者进行分工、并发与汇总。

## 核心要点

- **本质是职责拆分，不是盲目堆 Agent**：多 Agent 的价值来自边界清晰的角色分工，而不是把一个问题机械切成很多模型调用。
- **更低的上下文噪音**：每个 Agent 只保留与当前任务相关的 prompt 和工具描述，减少无关信息干扰。
- **更适合并发处理**：多个 Agent 可以并行探索不同子任务或方案，再由上层汇总结果。
- **更强的互审与纠错**：不同角色之间可以交叉检查、reviewer 化，而不只是单个 Agent 自我反思。
- **代价是编排复杂度上升**：任务拆分、状态同步、冲突处理、结果汇总、成本控制都会变得更难。

## 详细说明

### 为什么复杂 Agent 容易走向多 Agent
单 Agent 架构往往把所有工具描述、全部功能 prompt、所有角色要求都塞进一个 system prompt 里。这样虽然统一，但每次执行某个具体功能时都要把无关说明一起带上，既浪费 token，也提高误判概率。

多 Agent 架构的做法是按角色或任务域拆开：
- 路由 Agent 负责判断该找谁
- 专家 Agent 只处理某一类任务
- 审阅 Agent 负责检查结果

这样每个 Agent 的上下文更纯，决策面更窄，通常更稳定。

### 并行不是附赠品，而是核心收益
一旦任务被拆成多个独立子问题，多 Agent 就可以并行执行。对“查资料 + 写代码 + 跑测试 + 做审阅”这类可并行工作，整体 wall-clock 时间会明显下降。

### 多 Agent 不等于一定更省
多次模型调用会增加调度成本。如果拆分方式不合理，反而会出现：
- 子 Agent 边界不清，来回扯皮
- 汇总层成本过高
- 状态同步过多
- 最终 token 不降反升

所以多 Agent 更准确的理解是：**用编排复杂度换执行质量、并行性和上下文清洁度。**

### 真正难的是知识治理与路由，不是把 Agent 数量堆起来
用户提供截图文章《Agent 时代，工程师最值钱的能力是说“不”》补充了一个非常实战的视角：多 Agent 的门槛往往不在“写一个 debating 或 supervisor 机制”，而在如何让 expert 的知识来源稳定、边界清晰、激活规则可维护。相比“让 Manager 猜谁该被叫醒”，把 repo 内 markdown 作为唯一事实源，并用结构化 Expert Routing Table 来决定激活哪些子域 expert，通常更可靠，也更省上下文。

## 上下文

该概念是理解 [[concepts/subagent]]、[[concepts/agent-teams]]、[[patterns/supervisor-worker]] 与 [[products/langgraph]] 的上位框架。很多 Agent 产品从单一 loop 演进到团队协作，本质上都是在解决“一个上下文装不下所有职责”这个问题。

## 关联页面

- [[concepts/subagent]]
- [[concepts/agent-teams]]
- [[concepts/agent-loop]]
- [[concepts/harness-engineering]]
- [[concepts/engineering-sense]]
- [[patterns/supervisor-worker]]
- [[patterns/repo-native-expert-routing]]
- [[products/langgraph]]

## 参考文档

- 用户输入文章《LangGraph 和多 Agent 架构》（2026-04-16 收录）：总结多 Agent 的三类收益，包括 prompt 拆分、并行思考与多角色纠错
- 用户提供截图文章《Agent 时代，工程师最值钱的能力是说“不”》（2026-04-17 收录）
