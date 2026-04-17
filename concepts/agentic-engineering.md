# Agentic Engineering（智能体工程）

> 把 AI 放进结构化软件工程流程中运行的开发范式：人负责目标、约束和质量把关，AI 负责在既定流程里规划、执行、验证和迭代。

## 核心要点
- **本质是流程化，而不是一次性生成**：重点不在“让模型直接写出代码”，而在于把需求澄清、计划、实现、审查、部署、评审修复这些环节串成可重复流程。
- **人是编排者，AI 是执行者**：开发者从“亲自逐步操作”转向“定义目标、审批计划、确认部署、把关评审意见”。
- **关键节点必须有人审**：计划确认、代码审查、MR 评论提交、上线发布等高风险动作仍由人做最终判断，避免把 AI 当不受控自动机。
- **依赖 Skill / Command / MCP 分层协作**：Skill 承载业务流程，Command 作为轻入口，MCP 提供外部系统读写能力，三者组合成可编排工具链。
- **它与 Vibe Coding 的区别在纪律性**：Vibe Coding 偏“提示即祈祷”的快速生成；Agentic Engineering 则把 AI 嵌进有约束的工程系统里，用流程换可控性。

## 详细说明
### 从“直接生成”转向“结构化执行”
在这种范式里，AI 不再只是对着一句需求直接吐代码，而是先理解现状、提问澄清、形成计划、按任务执行、做自审、生成 MR、辅助 code review，再根据评论继续修复。真正重要的不是某一步有多聪明，而是整个链路是否可重复、可回放、可审核。

### 人机分工被重新定义
开发者并没有退出环路，而是把注意力从机械执行转向高价值决策。需求是否清晰、方案是否合理、部署是否安全、AI 的 review 建议是否准确，这些都仍然需要人判断。AI 被放在“高频、规则明确、容易模板化”的工作上，承担执行与整理，而不是替代最终责任人。

### 约束来自工程化外壳
文章给出的一个关键经验是：让 AI 可靠，不是单靠更强模型，而是给它一套工程外壳。`brainstorming`、`writing-plans`、`executing-plans`、`code-review`、`/create-mr`、`/fix-mr` 等技能和命令把“先澄清、再计划、再执行、再验证”的纪律前置成默认行为。

### 产出的不是代码片段，而是完整交付流
这种模式覆盖的不只是写代码，还包括需求单创建、分支初始化、日志定位、MR 描述生成、评审意见落点定位和修复闭环。换句话说，它关心的是“从需求到发布”的整条交付链，而不是某个局部生成动作。

## 上下文
该概念在微信公众号文章《从Vibe Coding到Agentic Engineering：重构后台开发全流程》中被明确拿来对比 [[concepts/vibercoding]]。文章用一个后台小需求的完整交付过程说明：AI 真正可落地的价值，不只是会写代码，而是能在有纪律的工程流程中持续承担执行工作。

## 关联页面
- [[concepts/vibercoding]]
- [[concepts/harness-engineering]]
- [[concepts/engineering-sense]]
- [[concepts/claude-code-skills]]
- [[concepts/mcp]]
- [[patterns/agent-workflow-calibration]]
- [[products/superpowers]]
- [[comparisons/vibercoding-vs-agentic-engineering]]

## 参考文档
- 微信公众号《从Vibe Coding到Agentic Engineering：重构后台开发全流程》（腾讯技术工程，作者署名 seanguo，2026-04-17，CDP 抓取）
