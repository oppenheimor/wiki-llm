# Wiki 目录

## 概念（concepts）

- [[concepts/hermes-agent]] — Nous Research推出的自进化本地AI智能体
- [[concepts/openclaw]] — 以工作区文件为核心的自托管AI智能体框架
- [[concepts/self-evolution]] — 智能体通过使用经验不断积累能力的范式
- [[concepts/layered-memory]] — Hermes Agent的分层持久化记忆体系
- [[concepts/agent-memory]] — 智能体记忆不是检索别名，而是管理过去如何进入现在的分层状态治理系统
- [[concepts/skill-system]] — 工作流自动抽象为可复用程序化技能的能力
- [[concepts/vibercoding]] — AI 可视化辅助编程范式
- [[concepts/rag-knowledge-base]] — 向量检索增强生成知识库
- [[concepts/parallel-subagent-debugging]] — 批量 bug 并行 subagent 修复模式
- [[concepts/claude-code-rules]] — Claude Code 配置的四层架构之规则层
- [[concepts/claude-code-skills]] — Claude Code 配置的四层架构之技能层
- [[concepts/claude-code-hooks]] — Claude Code 配置的四层架构之钩子层（含 memory-persistence、suggest-compact）
- [[concepts/claude-code-agents]] — Claude Code 配置的四层架构之代理层（47 个 sub-agent）
- [[concepts/claude-code-routines]] — Claude Code 云端自动化运行功能（定时/API/GitHub触发）
- [[concepts/claude-code-desktop]] — Claude Code 桌面端多会话并行重设计（含集成开发工具面板）
- [[concepts/reasoning-effort]] — 用 `effort` 统一调节模型推理深度、速度和 token 消耗的配置层
- [[concepts/tool-execution-pipeline]] — 把模型不可信的工具调用意图，经验证、Hook、权限和结果整形，转化为可控执行的分层管线
- [[concepts/prompt-cache]] — 通过缓存请求前缀避免重复处理稳定提示词与工具定义的运行时机制
- [[concepts/claude-identity-verification]] — Claude 平台针对特定能力与安全检查引入的身份验证机制
- [[concepts/harness-engineering]] — 将 LLM 集成到生产环境的完整基础设施体系（工具链/权限/上下文/安全边界）
- [[concepts/engineering-sense]] — Agent 时代的工程判断力：本质不是执行，而是对优先级、克制与“不做什么”的排序能力
- [[concepts/agentic-engineering]] — 把 AI 放进结构化软件工程流程中运行的开发范式
- [[concepts/agent-loop]] — Agent 的最小运行内核：模型在 while 循环中持续决定下一步行动
- [[concepts/agui-protocol]] — Agent 与图形界面之间传输流式文本、工具调用状态和结构化交互事件的协议层
- [[concepts/react-pattern]] — Reasoning / Acting / Observation 三段式 Agent 基础范式
- [[concepts/multi-agent-architecture]] — 将职责拆给多个专职 Agent，通过更纯净上下文、并行处理与互审提高复杂任务表现
- [[concepts/tokenization]] — 文本进入模型前的离散化过程，是窗口、计费和缓存的共同计量单位
- [[concepts/autoregressive-generation]] — 大模型逐 token 生成文本的基本机制，也是流式响应的底层来源
- [[concepts/kv-cache]] — Transformer 对历史 Key / Value 的缓存机制，决定长上下文的成本与延迟
- [[concepts/token-efficiency]] — 用更少 token 完成同等质量任务的能力，是 Agent 系统规模化与竞争力的核心约束
- [[concepts/constrained-decoding]] — 通过限制可选 token 保证结构化输出和工具调用合法性的解码技术
- [[concepts/mcp]] — Model Context Protocol，Agent 连接工具/数据的统一接入协议
- [[concepts/a2a-protocol]] — Google 主导的跨厂商 Agent-to-Agent 通信协议
- [[concepts/gep-protocol]] — 基因组进化协议：Agent 经验以基因胶囊形式可继承可进化
- [[concepts/agent-teams]] — Anthropic 多智能体协作机制（Team Lead + 持续 Teammate）
- [[concepts/subagent]] — 子智能体压缩模式："搜索的本质是压缩"
- [[concepts/metr-time-horizon]] — METR 时长度量：AI 独立完成任务时长每 4~7 个月翻一倍
- [[concepts/claude-to-im]] — 将 Claude Code 远程连接到飞书/Discord/Telegram 等 IM 平台的开源工具集
- [[concepts/agent-iam]] — Agent 时代的身份与访问管理：身份传播、无秘钥验证、上下文与意图感知授权

## 产品（products）

- [[products/nous-research]] — 开源优先、去中心化AI研究组织
- [[products/everything-claude-code]] — 154K stars 的 Claude Code 四层配置体系（Rules/Skills/Hooks/Agents）
- [[products/agent-shield]] — Claude Code 配置安全扫描工具（1282 项测试）
- [[products/pretext]] — 纯 JS/TS 文本测量与布局库，不碰 DOM 不触发 reflow
- [[products/learn-claude-code]] — Agent Harness 工程 0→1 教学项目（12 个渐进课程）
- [[products/claude-code-harness-analysis]] — 基于源码泄露快照的 Claude Code 工业级 Harness 架构逆向工程分析
- [[products/evomap]] — 基于 GEP 协议的 Agent 经验进化平台
- [[products/langgraph]] — LangChain 生态的图编排框架，用状态图组织 Agent、工具、分支、循环与中断恢复
- [[products/vercel-ai-sdk]] — 面向 AI 应用的全栈 SDK，提供 Data Stream Protocol 和前端消息消费抽象
- [[products/meoo]] — 阿里推出的 AI 应用生成产品，用自然语言和预置工作流快速生成网页与应用原型
- [[products/claude-agent-sdk]] — Anthropic 官方 Agent 开发 SDK，把 Claude Code 的运行时能力开放为 Python / TypeScript 库
- [[products/superpowers]] — 面向编程 Agent 的方法论型插件，把工程流程固化为自动触发的 skills
- [[products/gstack]] — 面向编码 Agent 的执行型技能工具箱，封装浏览器、QA、发布与护栏动作
- [[products/claude-managed-agents]] — Anthropic 托管式云端 Agent 运行平台，以 Agent/Environment/Session/Events 组织 hosted harness
- [[products/skillforge]] — 阿里云提出的垂直领域 Agent Skills 自进化框架

## 模式（patterns）

- [[patterns/claude-code-config-layers]] — Rules/Skills/Hooks/Agents 四层可配置结构模式
- [[patterns/llm-coding-discipline]] — LLM 编码四纪律（Think/Simplicity/Surgical/Goal-Driven）
- [[patterns/chrome-cdp-browser-ws-uuid]] — Chrome CDP 两种启用方式下 Browser WS 路径差异的陷阱与排查
- [[patterns/agent-always-on-host]] — 个人 Agent 想持续在线可用，宿主机必须 7×24 稳定运行
- [[patterns/agent-four-layers-2026]] — 2026 初 Agent 生态四层叠乘框架（大脑/手脚/组织/进化）
- [[patterns/model-native-agent-interface]] — 把内部复杂度翻译成模型熟悉表示，并按需渐进披露工具
- [[patterns/benchmark-first-agent-development]] — Agent 开发先做评估框架，再做功能和优化，用度量约束感觉驱动的迭代
- [[patterns/same-content-style-wall-screening]] — 用同一内容骨架生成多种静态样品并单页横向对比，先筛 UI 风格方向再深入实现
- [[patterns/prompt-as-system-design]] — Prompt 不是随手指令，而是把模块边界、抽象粒度和变化预期编码成系统设计
- [[patterns/repo-native-expert-routing]] — Repo 内文档作唯一事实源，配合结构化路由表激活对应 expert agent 的多 Agent 模式
- [[patterns/supervisor-worker]] — 一个主管负责路由和拆任务，多个专职 Worker 负责执行的多 Agent 协作模式
- [[patterns/agent-workflow-calibration]] — Agent 流程要按风险节点校准，而不是把所有好习惯写成僵硬命令链
- [[patterns/tool-aware-streaming-ui]] — 按文本、工具调用、工具结果等不同语义单元流式渲染 Agent UI 的模式

## 对比（comparisons）

- [[comparisons/hermes-agent-vs-openclaw]] — 两大自托管AI智能体框架的完整对比
- [[comparisons/chatbot-vs-copilot-vs-agent]] — 三种 AI 交互形态的控制权与自主性差异
- [[comparisons/vibercoding-vs-agentic-engineering]] — 快速生成范式与流程化交付范式的差异
