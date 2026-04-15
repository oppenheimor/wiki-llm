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
- [[concepts/claude-identity-verification]] — Claude 平台针对特定能力与安全检查引入的身份验证机制
- [[concepts/harness-engineering]] — 将 LLM 集成到生产环境的完整基础设施体系（工具链/权限/上下文/安全边界）
- [[concepts/agent-loop]] — Agent 的最小运行内核：模型在 while 循环中持续决定下一步行动
- [[concepts/react-pattern]] — Reasoning / Acting / Observation 三段式 Agent 基础范式
- [[concepts/tokenization]] — 文本进入模型前的离散化过程，是窗口、计费和缓存的共同计量单位
- [[concepts/autoregressive-generation]] — 大模型逐 token 生成文本的基本机制，也是流式响应的底层来源
- [[concepts/kv-cache]] — Transformer 对历史 Key / Value 的缓存机制，决定长上下文的成本与延迟
- [[concepts/constrained-decoding]] — 通过限制可选 token 保证结构化输出和工具调用合法性的解码技术
- [[concepts/mcp]] — Model Context Protocol，Agent 连接工具/数据的统一接入协议
- [[concepts/a2a-protocol]] — Google 主导的跨厂商 Agent-to-Agent 通信协议
- [[concepts/gep-protocol]] — 基因组进化协议：Agent 经验以基因胶囊形式可继承可进化
- [[concepts/agent-teams]] — Anthropic 多智能体协作机制（Team Lead + 持续 Teammate）
- [[concepts/subagent]] — 子智能体压缩模式："搜索的本质是压缩"
- [[concepts/metr-time-horizon]] — METR 时长度量：AI 独立完成任务时长每 4~7 个月翻一倍
- [[concepts/claude-to-im]] — 将 Claude Code 远程连接到飞书/Discord/Telegram 等 IM 平台的开源工具集

## 产品（products）

- [[products/nous-research]] — 开源优先、去中心化AI研究组织
- [[products/everything-claude-code]] — 154K stars 的 Claude Code 四层配置体系（Rules/Skills/Hooks/Agents）
- [[products/agent-shield]] — Claude Code 配置安全扫描工具（1282 项测试）
- [[products/pretext]] — 纯 JS/TS 文本测量与布局库，不碰 DOM 不触发 reflow
- [[products/learn-claude-code]] — Agent Harness 工程 0→1 教学项目（12 个渐进课程）
- [[products/claude-code-harness-analysis]] — 基于源码泄露快照的 Claude Code 工业级 Harness 架构逆向工程分析
- [[products/evomap]] — 基于 GEP 协议的 Agent 经验进化平台

## 模式（patterns）

- [[patterns/claude-code-config-layers]] — Rules/Skills/Hooks/Agents 四层可配置结构模式
- [[patterns/llm-coding-discipline]] — LLM 编码四纪律（Think/Simplicity/Surgical/Goal-Driven）
- [[patterns/chrome-cdp-browser-ws-uuid]] — Chrome CDP 两种启用方式下 Browser WS 路径差异的陷阱与排查
- [[patterns/agent-always-on-host]] — 个人 Agent 想持续在线可用，宿主机必须 7×24 稳定运行
- [[patterns/agent-four-layers-2026]] — 2026 初 Agent 生态四层叠乘框架（大脑/手脚/组织/进化）

## 对比（comparisons）

- [[comparisons/hermes-agent-vs-openclaw]] — 两大自托管AI智能体框架的完整对比
- [[comparisons/chatbot-vs-copilot-vs-agent]] — 三种 AI 交互形态的控制权与自主性差异
