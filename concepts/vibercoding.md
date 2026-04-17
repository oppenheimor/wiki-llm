# Vibercoding（AI 可视化辅助编程）

> 一种由 AI 主导的编程范式：开发者描述意图，AI 生成代码、调试并完成任务，人主要做验收和校正，而非手写代码。

## 核心特征

- **意图驱动**：开发者描述要做什么（what），而非如何实现（how）
- **AI 执行编码**：AI 生成、修改、调试代码
- **人做验收**：人负责确认结果是否符合预期，而非过程
- **适合非前端开发者**：生成 UI、图表、界面等可直观验收的成果

## 文章案例

- 《我是这么用 AI 的》里，作者用 Vibercoding 搭了一套**量化交易系统**，初步使用取得了不错收益。整个过程由 AI 主导编码。
- 《阿里下场做了中国版的 Lovable，好用到炸。》里，作者用 [[products/meoo]] 在三个多小时内做出一个普通话练习应用原型，并强调语音输入、自然语言迭代、框选界面局部修改和多人协作带来的高反馈速度。

## 与传统编程的对比

| 维度 | Vibercoding | 传统编程 |
|------|-------------|----------|
| 主导者 | AI | 开发者 |
| 核心活动 | 描述意图 + 验收结果 | 写代码 + 调试 |
| 代码掌控 | 低（AI 生成） | 高（手写） |
| 适合场景 | 快速原型、直观验收成果 | 精确控制、复杂底层逻辑 |

## 与 Agentic Engineering 的差异

微信公众号文章《从Vibe Coding到Agentic Engineering：重构后台开发全流程》给这个概念补了一个重要边界：Vibercoding 擅长把“我想要什么”快速变成能看的结果，但一旦进入生产交付，就会暴露出代码质量、审查流程和可维护性不足的问题。

相对地，[[concepts/agentic-engineering]] 关心的是把 AI 放进完整工程链路里，让它先澄清需求、再出计划、再执行、再验证，而不是一次性生成后靠运气通过。也就是说，Vibercoding 更像高反馈原型范式，Agentic Engineering 更像面向生产的流程范式。

## 关联页面

- [[concepts/rag-knowledge-base]] — AI 辅助的信息检索与知识管理
- [[concepts/parallel-subagent-debugging]] — AI 并行调试模式
- [[concepts/agentic-engineering]] — 以结构化工程流程约束 AI 执行的生产开发范式
- [[products/meoo]] — 面向中文语境的 AI 应用生成产品，文章把它当作 Vibecoding 的高反馈载体
- [[comparisons/vibercoding-vs-agentic-engineering]] — 快速生成范式与流程化交付范式的对比

## 参考文档

- 《我是这么用 AI 的》：微信公众号（2026-04-13）
- 《阿里下场做了中国版的 Lovable，好用到炸。》：AI产品阿颖，微信公众号（2026-04-16）
- 微信公众号《从Vibe Coding到Agentic Engineering：重构后台开发全流程》（腾讯技术工程，作者署名 seanguo，2026-04-17，CDP 抓取）
