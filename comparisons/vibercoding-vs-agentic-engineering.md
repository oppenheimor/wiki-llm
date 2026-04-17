# Vibercoding 与 Agentic Engineering 对比

> 两者都让 AI 深度参与开发，但前者强调“快速生成”，后者强调“流程约束下的持续交付”。

## 对比维度

| 对比维度 | Vibercoding | Agentic Engineering |
|----------|-------------|---------------------|
| 核心目标 | 快速做出可见结果 | 稳定完成可上线交付 |
| 主要交互 | 自然语言描述需求，直接生成 | 需求澄清、计划、执行、验证、评审的链式流程 |
| 人的角色 | 验收者、修正者 | 编排者、审批者、最终责任人 |
| AI 的角色 | 代码生成器 | 结构化流程中的执行型智能体 |
| 质量控制 | 主要靠结果验收 | 依赖计划审核、自审、MR 评审、发布把关 |
| 适合场景 | 原型、Demo、直观可验收任务 | 生产开发、团队协作、跨系统交付 |
| 主要风险 | 代码质量、可维护性、遗漏流程 | token 成本高、流程更重、需要更完整工具链 |

## 各自优势

### Vibercoding
- 上手快，反馈周期短。
- 适合 UI、原型、探索性需求。
- 对非工程背景用户更友好。

### Agentic Engineering
- 更适合需要审查、部署、回归验证的真实研发流程。
- 能把需求、代码、MR、日志和评审收敛在一个连续工作流里。
- 更容易沉淀为团队方法论，而不是个人技巧。

## 选型指南
如果任务的目标是“尽快做出一个能看、能试的结果”，[[concepts/vibercoding]] 往往更合适；如果目标是“让 AI 真正进入研发交付链”，并且需要计划、review、部署和修复闭环，那么 [[concepts/agentic-engineering]] 更贴近实际生产环境。

很多团队的真实路径不是二选一，而是先用 Vibercoding 探索方向，再把有效模式升级成 Agentic Engineering 的标准流程。

## 关联页面
- [[concepts/vibercoding]]
- [[concepts/agentic-engineering]]
- [[concepts/harness-engineering]]
- [[patterns/agent-workflow-calibration]]
- [[products/superpowers]]

## 参考文档
- 微信公众号《从Vibe Coding到Agentic Engineering：重构后台开发全流程》（腾讯技术工程，作者署名 seanguo，2026-04-17，CDP 抓取）
