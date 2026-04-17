# Harness Engineering

> 以可控方式将大语言模型（LLM）集成到生产环境中的完整基础设施与流程体系，覆盖工具链、权限、上下文管理、多智能体协作与安全边界。

## 核心要点
- **模型与 Harness 分离**：模型决定做什么，Harness 负责在什么条件下安全地执行（工具、权限、上下文、监控）。
- **安全联锁与分级防御**：借鉴化工控制论的安全联锁理念，通过内容扫描、脚本执行守卫、Worktree 隔离等多层防护实现“故障安全”。
- **按需学习与知识分级**：技能与上下文按需加载，利用三层压缩（对话→摘要→持久化）管理有限窗口。
- **缓存友好的上下文布局**：system prompt、工具定义、动态上下文和附件的排布，会直接影响 prompt cache 命中率与长会话成本。
- **多智能体编排**：Team Lead + 持续存在的 Teammate 协同，通过 Git 锁与 Worktree 实现并行探索与冲突避免。
- **可编程的触发与调度**：支持定时、API、事件驱动三种触发模式，将一次性任务转化为可观测、可重放的流程。
- **Harness 已开始产品化为托管平台**：不仅能作为本地 CLI 或 SDK 能力出现，也能以 hosted runtime 的形式对外提供。
- **本质仍是老工程问题的 AI 语境重述**：工具选择、信息注入、错误拦截、跨会话记忆和运行环境设计，并不会因为名字从 prompt/context 变成 harness 就自动变成一门新学科。

## 详细说明
### 模型即能力，Harness 即环境
模型本身并不具备“安全操作世界”的能力；Harness 通过封装工具、约束权限、记录审计轨迹，让模型在沙箱中发挥能力而不越界。Claude Code 的源码展示了从单循环到完整 Harness 的演进：QueryEngine 是循环核心，Tool 系统是双手，Permission 钩子是安全边界，Team 系统是组织架构，Memory 是持久化记忆。

### 分层防御与实践
- **内容扫描**：在写文件前检查危险调用（如 `shutil.rmtree`），拦截已知破坏性模式。
- **脚本执行守卫**：禁止执行当前会话刚写入的脚本，避免自我注入。
- **Worktree 隔离**：每个任务或子智能体在独立工作区操作，完成后通过 Git Merge 合并，减少主分支污染。
- **权限分级（auto/plan/default/bypass）**：根据风险与信任动态调整审批粒度。
- **工具执行管线**：一次工具调用通常要经过 schema 验证、业务校验、输入标准化、Pre/Post Hook、权限判定、结果预算与错误整形，核心目标不是“能调用工具”，而是“能在失败时被模型自我纠正”。

### 上下文与记忆工程
- **三层压缩**：对话级 → 摘要级 → 持久化（memdir/tasks），确保长周期任务可恢复且不耗尽窗口。
- **子智能体独立上下文**：通过 `AgentTool` 创建的 sub-agent 拥有独立 `messages[]`，主会话仅接收结果摘要，防止噪音污染。
- **prompt cache 约束布局**：稳定前缀与动态后缀的分区，不只是性能优化技巧，而是长 session Agent 是否可持续运行的前提条件。

### Harness as a Service
用户输入文章《Harness Engineering 完全指南》把 Claude Code SDK 一类产品总结为 HaaS（Harness as a Service）：开发者不再从零写工具循环，而是在现成 Harness 上叠加自己的提示、工具与约束。进一步往前走，Claude Managed Agents 这类托管平台则把 Harness 本身直接做成云服务，把环境、会话和事件流都产品化。

### 它不是新瓶装出来的新学问
很多所谓的 prompt engineering、context engineering、harness engineering，讨论的其实都是同一类问题：怎样给模型提供正确的信息、工具和边界，让它在失败时可控、在跨会话时可恢复。用户提供截图文章《Agent 时代，工程师最值钱的能力是说“不”》强调，真正稀缺的不是为这些事起新名字，而是把传统软件工程里的关注点分离、文档治理、约束前移、评估先行，扎实落到 Agent 工作环境里。

### 多智能体协调模式
支持 Pipeline、Fan-out/Fan-in、Expert Pool、Producer-Reviewer、Supervisor、Hierarchical Delegation 六种模式，通信载体包括异步邮箱、共享任务列表与事件总线。

## 上下文
本概念作为理解 Claude Code 与类似系统架构的公共词汇；在 [[products/everything-claude-code]]、[[patterns/agent-four-layers-2026]]、[[products/claude-code-hooks-analysis]] 中均有体现。

## 关联页面
- [[concepts/agent-loop]]
- [[concepts/react-pattern]]
- [[concepts/tokenization]]
- [[concepts/autoregressive-generation]]
- [[concepts/kv-cache]]
- [[concepts/constrained-decoding]]
- [[concepts/agui-protocol]]
- [[concepts/multi-agent-architecture]]
- [[concepts/agent-teams]]
- [[concepts/subagent]]
- [[concepts/engineering-sense]]
- [[concepts/token-efficiency]]
- [[concepts/prompt-cache]]
- [[patterns/tool-aware-streaming-ui]]
- [[concepts/tool-execution-pipeline]]
- [[patterns/supervisor-worker]]
- [[patterns/claude-code-config-layers]]
- [[patterns/agent-four-layers-2026]]
- [[patterns/benchmark-first-agent-development]]
- [[patterns/prompt-as-system-design]]
- [[patterns/repo-native-expert-routing]]
- [[products/everything-claude-code]]
- [[products/vercel-ai-sdk]]
- [[products/superpowers]]
- [[products/gstack]]
- [[products/claude-managed-agents]]
- [[products/skillforge]]
- [[products/langgraph]]
- [[concepts/claude-code-routines]]
- [[concepts/mcp]]

## 参考文档
- Claude Code 源码快照（2026-03-31）：https://github.com/instructkr/claude-code
- 微信文章《从Harness角度对Claude Code源码深度解读》：https://www.51cto.com/article/839733.html
- 微信文章《刚刚！Claude Code 推出 Routines》：https://mp.weixin.qq.com/s/fjGd3mBJ2cHnR7Ctmx7vmA
- 微信文章《Harness Engineering 实战：harness的最佳理解方式》：https://mp.weixin.qq.com/s/zafqdw8m5tYY8E49x-vf9g
- 用户输入文章《Harness Engineering 完全指南》（2026-04-17 收录）
- 用户输入文章《一次工具调用背后经历了什么？以 Claude Code 为例展开聊聊》（2026-04-17 收录）
- 用户提供截图文章《Agent 时代，工程师最值钱的能力是说“不”》（2026-04-17 收录）
