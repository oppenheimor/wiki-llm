# Wiki 操作日志

## 2026-04-17: 收录 5 篇 Agent 文章（Harness / Context / Skills / Managed Agents / SkillForge）

**来源**：
- https://mp.weixin.qq.com/s/junA24jW10KXQEDUdCcCKA （寒日，微信公众号，2026-04-13，CDP 抓取）
- https://mp.weixin.qq.com/s/kpiOa4oacxTzWj1rhXgnHQ （晨思片刻，作者署名 技术分享，微信公众号，2026-04-04，CDP 抓取）
- https://mp.weixin.qq.com/s/PGoyLb32J5nSLCmXt9XoJg （刷屏AI，作者署名 飞哥，微信公众号，2026-04-10，CDP 抓取）
- https://mp.weixin.qq.com/s/A_ksLCNmIL4lXLcZeVSPsQ （技术极简主义，作者署名 兔兔AGI，微信公众号，2026-04-15，CDP 抓取）
- https://mp.weixin.qq.com/s/By3zvI4H8Il58iOK4e7ONg （AI应用研究Lab，作者署名 Leon，微信公众号，2026-04-15，CDP 抓取）
- https://github.com/obra/superpowers （GitHub README，2026-04-17 查阅）
- https://github.com/garrytan/gstack （GitHub README，2026-04-17 查阅）
**新增页面**：
- concepts/prompt-cache.md — 把“稳定前缀缓存”从 Claude Code 具体实现上升为通用 Agent 运行时概念
- products/superpowers.md — 面向编程 Agent 的方法论型 skill 体系
- products/gstack.md — 面向编码 Agent 的执行型 slash-command 工具箱
- products/claude-managed-agents.md — Anthropic 托管式 hosted harness 平台
- products/skillforge.md — 企业级 Agent Skills 自进化框架
**更新页面**：
- concepts/harness-engineering.md：补充 prompt cache 约束与 Harness as a Service / hosted harness 的产品化路径
- concepts/claude-code-skills.md：补充“方法论层 vs 执行层” skills 组织方式，以及企业场景里的 skill 生命周期视角
- products/claude-code-harness-analysis.md：补充 Claude Code 上下文拼装、结果落盘阈值和 prompt cache 作为上位约束
- products/claude-agent-sdk.md：补充与 Claude Managed Agents 的边界对照
- index.md：新增 1 个 concept 入口与 4 个 product 入口
**新增交叉引用**：
- prompt-cache ↔ kv-cache / token-efficiency / harness-engineering / claude-code-harness-analysis / claude-agent-sdk / claude-managed-agents
- superpowers ↔ claude-code-skills / skill-system / harness-engineering / llm-coding-discipline / gstack
- gstack ↔ claude-code-skills / harness-engineering / tool-aware-streaming-ui / superpowers
- claude-managed-agents ↔ harness-engineering / agent-loop / mcp / multi-agent-architecture / prompt-cache / claude-agent-sdk
- skillforge ↔ claude-code-skills / skill-system / harness-engineering / agent-memory / rag-knowledge-base
**审计备注**：
- `Harness Engineering 完全指南` 与 `Claude Code 上下文管理机制` 的稳定价值不在“又一篇教程”，而在于把上下文布局、缓存边界和结果落盘从使用经验提升为可复用的运行时设计知识
- `superpowers + gstack` 文最值得沉淀的是“方法论层 / 执行层”分工，而不是逐条安装命令；产品页已用 GitHub README 做一手校验
- `Claude Managed Agents` 当前在本地 Anthropic 文档索引中未直接检索到专门条目，页面先按文章中较稳定的四原语与 hosted harness 定位沉淀，后续若补到官方专门文档可再增强
- SkillForge 暂以“企业级 skill 自进化框架”收录；若后续拿到论文原文或官方项目页，适合继续补实验设计与更严格的一手来源

## 2026-04-17: 收录《Configure your effort level》

**来源**：用户输入短文（内容包括 Opus 4.7 使用 adaptive thinking 取代 thinking budgets、通过 `/effort` 调整 `effort`、`max` 仅对当前 session 生效、其他档位会跨 session 持久）
**新增页面**：
- concepts/reasoning-effort.md — 把 thinking budget 的底层资源调参抽象为更高层的“推理强度”配置概念
**更新页面**：
- index.md：新增 1 个 concept 入口（reasoning-effort）
**新增交叉引用**：
- reasoning-effort ↔ agent-loop / tokenization / claude-code-rules / claude-agent-sdk
**审计备注**：
- 本次材料信息量较短，稳定知识焦点是“effort 作为 thinking budget 的产品化替代抽象”，而不是具体推荐使用哪一档
- Wiki 里暂未发现现成页面专门承接 Claude / Anthropic 语境下的推理强度配置，因此新建概念页比硬塞进现有条目更干净

## 2026-04-17: 收录《一次工具调用背后经历了什么？以 Claude Code 为例展开聊聊》

**来源**：用户输入文章（主题涵盖 Function Calling 之后的工具执行管线、Zod schema 校验、业务校验、输入补全与缓存、PreToolUse/PostToolUse Hook、权限分层、结果截断、面向模型的错误设计、OpenClaw 事件驱动、OpenCode Batch Tool）
**新增页面**：
- concepts/tool-execution-pipeline.md — 将“模型输出工具 JSON 不可信”抽象为一条可复用的工程概念：验证、校准、Hook、授权、执行、结果整形
**更新页面**：
- concepts/claude-code-hooks.md：补充 Hook 在单次工具执行中的前置/后置位置，而不只限于会话级自动化
- concepts/harness-engineering.md：补充工具执行管线作为 Harness 分层防御的一部分
- products/claude-code-harness-analysis.md：补充 Claude Code 单次工具调用的处理层次，以及结果预算属于上下文工程
- products/claude-agent-sdk.md：补充与 tool-execution-pipeline 的映射，明确 SDK 暴露的是可编程执行运行时
- index.md：新增 1 个 concept 入口（tool-execution-pipeline）
**新增交叉引用**：
- tool-execution-pipeline ↔ harness-engineering / claude-code-hooks / constrained-decoding / openclaw / model-native-agent-interface / tool-aware-streaming-ui / claude-code-harness-analysis / claude-agent-sdk
- claude-code-hooks ↔ tool-execution-pipeline
- harness-engineering ↔ tool-execution-pipeline
- claude-code-harness-analysis ↔ tool-execution-pipeline
- claude-agent-sdk ↔ tool-execution-pipeline
**审计备注**：
- 本次沉淀的稳定知识焦点不是某个具体参数名或阈值，而是“模型输入不可信”下的分层联锁设计
- OpenCode 的 Batch Tool 与 OpenClaw 的事件驱动架构被吸收到模式页中，作为并发与扩展形态的对照，而未单独膨胀成信息密度不足的产品页

## 2026-04-16: 收录《阿里下场做了中国版的 Lovable，好用到炸。》

**来源**：https://mp.weixin.qq.com/s/oyxud3tAmvSR868NqK9mRA （AI产品阿颖，微信公众号，2026-04-16，CDP 抓取）以及 Meoo 官网 https://meoo.com
**新增页面**：
- products/meoo.md — 阿里推出的 AI 应用生成产品，沉淀其“自然语言生成应用 + 文件驱动生成 + 预置案例工坊”的稳定定位
**更新页面**：
- concepts/vibercoding.md：补充 Meoo 作为 Vibecoding 高反馈载体的案例，并增加产品关联
- index.md：新增 1 个产品入口（meoo）
**新增交叉引用**：
- meoo ↔ vibercoding / multi-agent-architecture / harness-engineering
- vibercoding ↔ meoo
**审计备注**：
- 官方站点用于确认稳定事实：产品名称、Meta 描述、首页预置分类与案例
- 微信文章主要用于补充体验视角：Lovable 类比、蜂群式多智能体、Skill 复用、可视化修改、多人协作与阿里云整合

## 2026-04-16: 收录《AGUI 协议：Vercel AI SDK + LangChain 实现流式组件渲染 已付费》

**来源**：用户输入文章（含 Vercel AI SDK Data Stream Protocol、`@ai-sdk/langchain`、NestJS SSE、React `useChat`、Streamdown 与工具组件渲染示例）
**新增页面**：
- concepts/agui-protocol.md — Agent 与图形界面之间的协议层：把纯文本流升级为可区分文本、tool input、tool output 和状态事件的结构化交互流
- products/vercel-ai-sdk.md — 面向 AI 应用的全栈 SDK，沉淀其真正长期价值：统一流式协议与前端消息消费抽象，而不只是“又一个调模型包”
- patterns/tool-aware-streaming-ui.md — 按语义单元而非整段字符串渲染 Agent UI 的模式，强调文本 part 与工具 part 分层处理
**更新页面**：
- concepts/agent-loop.md：补充 AGUI / tool-aware-streaming-ui / vercel-ai-sdk 的关联，强调 Agent loop 的“观察轨迹”也需要面向用户可视化
- concepts/harness-engineering.md：补充 UI 协议层作为 Harness 对外可观测面的组成部分
- patterns/model-native-agent-interface.md：补充 AGUI 与 tool-aware-streaming-ui 的关联，说明“模型友好接口”与“用户友好交互协议”是两层不同抽象
- index.md：新增 1 个概念入口、1 个产品入口、1 个模式入口
**新增交叉引用**：
- agui-protocol ↔ agent-loop / harness-engineering / constrained-decoding / tool-aware-streaming-ui / vercel-ai-sdk / model-native-agent-interface
- vercel-ai-sdk ↔ agui-protocol / tool-aware-streaming-ui / agent-loop / harness-engineering / langgraph
- tool-aware-streaming-ui ↔ agui-protocol / vercel-ai-sdk / agent-loop / harness-engineering / model-native-agent-interface

## 2026-04-16: 收录《LangGraph 和多 Agent 架构》

**来源**：用户输入文章（含 LangGraph / LangChain / Supervisor-Worker 代码示例）
**新增页面**：
- products/langgraph.md — LangChain 生态里的图编排框架，沉淀 StateGraph、条件路由、循环、checkpointer、中断恢复与预构建 agent loop 的长期价值
- concepts/multi-agent-architecture.md — 多 Agent 架构的上位概念，解释 prompt 拆分、并行处理、多角色互审三类主要收益及其代价
- patterns/supervisor-worker.md — 最常见的多 Agent 协作模式，一个主管调度多个专职 Worker
**更新页面**：
- concepts/agent-loop.md：补充与 multi-agent-architecture / langgraph 的关联
- concepts/agent-teams.md：补充与 multi-agent-architecture / supervisor-worker 的关联
- concepts/harness-engineering.md：补充 multi-agent-architecture / supervisor-worker / langgraph 的关联
- products/learn-claude-code.md：补充与 multi-agent-architecture 的关联
- patterns/agent-four-layers-2026.md：补充与 multi-agent-architecture / supervisor-worker 的关联
- index.md：新增 1 个产品入口、1 个概念入口、1 个模式入口
**新增交叉引用**：
- langgraph ↔ agent-loop/multi-agent-architecture/supervisor-worker/harness-engineering/subagent/agent-teams
- multi-agent-architecture ↔ subagent/agent-teams/agent-loop/harness-engineering/supervisor-worker/langgraph
- supervisor-worker ↔ multi-agent-architecture/subagent/agent-teams/harness-engineering/langgraph

## 2026-04-15: 收录 3 篇 Agent 文章（OpenClaw 安全 / Notion Custom Agents / Hermes 后续配置）

**来源**：
- https://mp.weixin.qq.com/s/6WjEsaPbB3w19G_lP2pkog （字节跳动技术团队，作者署名 火山AI安全，微信公众号，2026-04-15，CDP 抓取）
- https://mp.weixin.qq.com/s/66dwBCc1mKfatEQQrayjtA （Founder Park，微信公众号，2026-04-15，CDP 抓取）
- https://mp.weixin.qq.com/s/mk9vx9dtzyguqPDPmY91zQ （梦朝思夕技术与管理博客，微信公众号，2026-04-15，CDP 抓取）
**新增页面**：
- concepts/agent-iam.md — Agent 时代身份与访问管理的上位框架：身份传播、无秘钥验证、上下文感知、意图感知授权
- patterns/model-native-agent-interface.md — 将内部复杂数据模型翻译成模型熟悉表示，并按工具规模做渐进式披露的接口设计模式
**更新页面**：
- concepts/openclaw.md：补入从 Agent IAM 视角理解 OpenClaw 风险放大的解释，并关联上位概念
- concepts/hermes-agent.md：补入安装完成后的真实扩展面，包括 `SOUL.md`、外部记忆、Session Search、web_search、Camofox、Gateway 与 MCP
- concepts/layered-memory.md：补充外接 memory provider 与 Session Search 对分层记忆的实际补足关系
- concepts/mcp.md：补充 MCP 与 CLI 的设计张力，强调“受控接口层”与“可自修复执行面”的差异
- index.md：新增 1 个 concept 入口与 1 个 pattern 入口
**新增交叉引用**：
- agent-iam ↔ openclaw / harness-engineering / mcp / claude-identity-verification
- model-native-agent-interface ↔ mcp / constrained-decoding / harness-engineering
- mcp ↔ model-native-agent-interface
- openclaw ↔ agent-iam
**审计备注**：
- OpenClaw 安全文更适合沉淀为通用的 Agent IAM 上位概念，而不是只在 OpenClaw 页面追加事故罗列
- Notion 文最有复用价值的是“模型友好接口”设计原则，而不是产品八卦或访谈逐段摘抄
- Hermes 文以现有页面补丁为主，保留长期稳定的配置面，不机械收录易过期的安装细节

## 2026-04-15: 收录《龙虾退热后，爱马仕来了》

**来源**：https://mp.weixin.qq.com/s/AA2fbMkT1ECwBlVcgC-YkA （AGI Hunt，微信公众号，2026-04-15，CDP 抓取）
**新增页面**：
- patterns/agent-always-on-host.md — 个人 Agent 想从“本地软件”变成“持续在线助理”，需要 7×24 在线宿主机
**更新页面**：
- concepts/hermes-agent.md：补充 `hermes claw migrate` 迁移信息与宿主机前提
- concepts/openclaw.md：补充 Gateway / HEARTBEAT 对持续在线宿主机的依赖
- comparisons/hermes-agent-vs-openclaw.md：补充“共同前提：宿主机先于框架选择”与宿主机对比维度
- index.md：新增 1 个 pattern 入口（agent-always-on-host）
**新增交叉引用**：
- agent-always-on-host ↔ hermes-agent/openclaw/hermes-agent-vs-openclaw/claude-code-routines
- hermes-agent ↔ agent-always-on-host
- openclaw ↔ agent-always-on-host
- hermes-agent-vs-openclaw ↔ agent-always-on-host
**审计备注**：
- 文章中关于 Hermes 与 OpenClaw 的框架差异主要作为现有页面的增量来源
- 文章中关于七牛云轻量服务器的厂商推广信息未直接沉淀为稳定知识，抽象为更长期有效的“7×24 在线宿主机”模式
**未执行项**：
- 飞书 Wiki / 多维表格同步未执行：当前 `lark-cli` 缺少 user authorization 与 bitable 读取权限

## 2026-04-15: 收录《疯了……Claude 最强风控：验你实名身份证！》

**来源**：https://mp.weixin.qq.com/s/2v8pMIREoBgAI62fyZ96FA （AGI Hunt，微信公众号，2026-04-15，CDP 抓取）
**新增页面**：
- concepts/claude-identity-verification.md — Claude 平台引入的身份验证机制（特定能力访问 / 平台完整性检查 / 安全与合规）
**更新页面**：
- index.md：补充 1 个新概念入口（claude-identity-verification）
**新增交叉引用**：
- claude-identity-verification ↔ claude-code-routines/harness-engineering/rag-knowledge-base
**审计备注**：
- 已用 Anthropic 官方帮助中心《Identity verification on Claude》核实验证触发条件、材料要求、Persona 分工与数据使用边界
- 已用 OpenAI 官方帮助中心《API Organization Verification》核实组织验证的证件要求、90 天限制与能力解锁范围
**未执行项**：
- 飞书 Wiki / 多维表格同步未执行：当前 `lark-cli` 缺少 user authorization 与 bitable 读取权限

## 2026-04-15: 收录《过了个年，AI 圈变天了？但没人告诉你为什么》

**来源**：https://mp.weixin.qq.com/s/z7zNi_DayzevcTe0EUTv5g （歸藏的AI工具箱，微信公众号，2026-02-25，CDP 抓取）
**新增页面**：
- patterns/agent-four-layers-2026.md — 2026 初 Agent 四层叠乘框架（主论点）
- concepts/mcp.md — Model Context Protocol
- concepts/a2a-protocol.md — Agent-to-Agent 协议
- concepts/gep-protocol.md — 基因组进化协议
- concepts/agent-teams.md — Agent Teams 多智能体协同
- concepts/subagent.md — SubAgent 压缩模式
- concepts/metr-time-horizon.md — METR 任务时长度量
- products/evomap.md — 经验进化平台
**更新页面**：
- concepts/openclaw.md：补充 Peter Steinberger 身份、OpenAI 收购事实、GUI 自动化、HEARTBEAT 心跳机制；修正关联页面指向已存在条目
- index.md：新增 7 个 concepts、1 个 product、1 个 pattern 入口
**新增交叉引用**：
- agent-four-layers-2026 ↔ mcp/a2a-protocol/gep-protocol/agent-teams/subagent/metr-time-horizon/openclaw/evomap/claude-code-skills/parallel-subagent-debugging/claude-code-config-layers
- mcp ↔ a2a-protocol/claude-code-skills/openclaw
- gep-protocol ↔ evomap/self-evolution/claude-code-skills
- agent-teams ↔ subagent/parallel-subagent-debugging/claude-code
- subagent ↔ agent-teams/parallel-subagent-debugging/claude-code-agents

## 2026-04-15: 收录 Chrome CDP Browser WS UUID 陷阱排查经验

**来源**：本机实际排查（cdp-proxy.mjs 时灵时不灵问题定位与修复）
**新增页面**：
- patterns/chrome-cdp-browser-ws-uuid.md
**更新页面**：
- index.md：新增 chrome-cdp-browser-ws-uuid 模式入口
**新增交叉引用**：
- chrome-cdp-browser-ws-uuid → concepts/claude-code-skills

## 2026-04-15: 收录 forrestchang/andrej-karpathy-skills 的 CLAUDE.md

**来源**：https://github.com/forrestchang/andrej-karpathy-skills/blob/main/CLAUDE.md（curl raw 抓取，2026-04-15）
**新增页面**：
- patterns/llm-coding-discipline.md
**更新页面**：
- index.md：新增 llm-coding-discipline 模式入口
**新增交叉引用**：
- LLM Coding Discipline ↔ Claude Code Rules（属于规则层的具体实例）
- LLM Coding Discipline ↔ Claude Code Config Layers（四层架构归位）

## 2026-04-15: 收录 shareAI-lab/learn-claude-code GitHub 仓库

**来源**：https://github.com/shareAI-lab/learn-claude-code（通过 Jina 抓取 README，2026-04-15）
**新增页面**：
- products/learn-claude-code.md
**更新页面**：
- index.md：新增 learn-claude-code 产品入口
**新增交叉引用**：
- Learn Claude Code ↔ Everything Claude Code（教学 vs 使用的互补关系）
- Learn Claude Code ↔ Claude Code Routines（s07-s12 的云端版本类比）
- Learn Claude Code ↔ Hermes Agent（框架对比）

## 2026-04-15: 收录 chenglou/pretext GitHub 仓库

**来源**：https://github.com/chenglou/pretext（通过 Jina 抓取 README，2026-04-15）
**新增页面**：
- products/pretext.md
**更新页面**：
- index.md：新增 pretext 产品入口
**新增交叉引用**：
- 暂无（首个文本测量/布局领域实体，待后续相关页面收录后补交叉引用）

## 2026-04-15: 收录《刚刚！Claude Code 两连发：Routines 让 AI 替你值班，桌面端一个窗口并行跑多任务》

**来源**：微信公众号文章（通过 CDP 抓取，2026-04-15）
**新增页面**：
- concepts/claude-code-desktop.md
**更新页面**：
- concepts/claude-code-routines.md：补充时区自动换算、API 触发上下文、GitHub 事件过滤条件、SDK 跨语言移植场景、身份归属与权限最小化注意事项、"Claude Code on the web" 前置条件
- index.md：新增 claude-code-desktop 入口
**新增交叉引用**：
- Claude Code Desktop ↔ Claude Code Routines（同日发布的「并行」双更新）

## 2026-04-15: 收录《刚刚，Claude Code 推出 Routines，让 AI 自动帮你值夜班》

**来源**：微信公众号文章（通过 CDP 抓取，2026-04-15）
**新增页面**：
- concepts/claude-code-routines.md
**更新页面**：
- index.md：补充 1 个新概念入口（claude-code-routines）
- products/everything-claude-code.md：补充与 Routines 的交叉引用
**新增交叉引用**：
- Claude Code Routines ↔ Everything Claude Code（ECC 四层架构的自然延伸）

## 2026-04-14: 收录《154K Star！Anthropic黑客松冠军的Claude Code配置大公开》

**来源**：微信公众号文章（通过 CDP 抓取，2026-04-14）
**新增页面**：
- products/everything-claude-code.md
- concepts/claude-code-rules.md
- concepts/claude-code-skills.md
- concepts/claude-code-hooks.md
- concepts/claude-code-agents.md
- patterns/claude-code-config-layers.md
- products/agent-shield.md
**更新页面**：
- index.md：补充 7 个新入口（新概念 4 个 + 产品 2 个 + 模式 1 个）
- concepts/hermes-agent.md：补充与 Everything Claude Code 的交叉引用
**新增交叉引用**：
- Everything Claude Code ↔ Claude Code Rules/Skills/Hooks/Agents（四层架构内部）
- Claude Code Hooks ↔ Layered Memory（memory-persistence 与分层记忆的关联）
- Claude Code Skills ↔ Skill System（技能抽象思路关联）
- Claude Code Agents ↔ Hermes Agent（Agent 协调架构关联）
- Claude Code Config Layers ↔ Everything Claude Code
- AgentShield ↔ Everything Claude Code

## 2026-04-14: 收录《我是这么用 AI 的》

**来源**：微信公众号文章（通过 CDP 抓取，2026-04-13）
**新增页面**：
- concepts/vibercoding.md
- concepts/rag-knowledge-base.md
- concepts/parallel-subagent-debugging.md
**更新页面**：
- index.md：补充 3 个新概念入口
- [[concepts/hermes-agent]]：补充"并行任务处理"能力描述
**新增交叉引用**：
- Vibercoding ↔ RAG Knowledge Base
- Vibercoding ↔ Parallel Subagent Debugging
- Parallel Subagent Debugging ↔ Hermes Agent
- Parallel Subagent Debugging ↔ Self-Evolution
- RAG Knowledge Base ↔ Hermes Agent

**图片补充（同一日）**：
- 更新 [[concepts/layered-memory]]：嵌入官方分层记忆架构图（来源：Hermes Agent 官方文档），补充四层结构表格

## 2026-04-14: 收录《Hermes Agent vs OpenClaw：架构差异与最佳应用场景解析》

**来源**：微信公众号文章（通过 CDP 抓取）
**新增页面**：
- concepts/hermes-agent.md
- concepts/openclaw.md
- concepts/self-evolution.md
- concepts/layered-memory.md
- concepts/skill-system.md
- products/nous-research.md
- comparisons/hermes-agent-vs-openclaw.md
**更新页面**：无（全新 Wiki）
**新增交叉引用**：
- Hermes Agent ↔ OpenClaw（对比页 + 互相引用）
- Hermes Agent ↔ Nous Research
- Hermes Agent ↔ Self-Evolution
- Hermes Agent ↔ Layered Memory
- Hermes Agent ↔ Skill System
- OpenClaw ↔ Skill System
- Self-Evolution ↔ Layered Memory
- Self-Evolution ↔ Skill System

## 2026-04-15: 收录 Claude Code Routines 新增文章 + Harness Engineering + Claude Code 源码分析 + Claude-to-IM

**来源**：
- 微信公众号（CDP 抓取）：Claude 新功能 Routines：关上笔记本，也能 7×24 干活（2026-04-15）
- 微信公众号（CDP 抓取）：Harness Engineering 实战：harness的最佳理解方式（陆徐洲，2026-04-15）
- 51CTO（CDP 抓取）：从Harness角度对Claude Code源码深度解读（2026-04-15）
- 微信公众号（CDP 抓取）：让你的 ClaudeCode 秒变 Openclaw（龙虾），连接飞书、Discord 远程控制（2026-04-15）
- 官方文档（WebFetch）：https://code.claude.com/docs/en/agent-teams（已存在于 Wiki，无需新建）

**新增页面**：
- concepts/harness-engineering.md — 将 LLM 集成到生产环境的完整基础设施体系（模型/Harness 分离原则、安全联锁、上下文工程、六种多智能体模式）
- products/claude-code-harness-analysis.md — 基于源码泄露快照的 Claude Code 工业级 Harness 架构逆向工程（1,900 文件、512K 行 TypeScript，src/tools 到 src/plugins 的完整子系统拆解）
- concepts/claude-to-im.md — Claude-to-IM/Claude-to-IM-skill 开源工具集（Skill 安装即用 + SDK 面向开发者）

**更新页面**：
- concepts/claude-code-routines.md：补充每日运行上限（Pro 5/Max 15/Team&Enterprise 25）、身份归属注意事项；新增参考来源
- concepts/agent-teams.md：补充 harness-engineering 和 claude-code-harness-analysis 交叉引用
- products/everything-claude-code.md：补充 harness-engineering 和 claude-code-harness-analysis 交叉引用
- patterns/agent-four-layers-2026.md：补充 harness-engineering 交叉引用
- index.md：新增 3 个入口（harness-engineering + claude-to-im + claude-code-harness-analysis）

**新增交叉引用**：
- harness-engineering ↔ agent-teams/claude-code-routines/everything-claude-code/claude-code-harness-analysis/mcp/agent-four-layers-2026
- claude-code-harness-analysis ↔ harness-engineering/agent-teams/subagent/claude-code-routines/everything-claude-code/learn-claude-code/agent-four-layers-2026
- claude-to-im ↔ claude-code-routines/mcp
- claude-code-routines ↔ harness-engineering/claude-code-harness-analysis
- agent-teams ↔ harness-engineering/claude-code-harness-analysis

## 2026-04-15: 收录《从 ChatBot 到 Agent：一个 while 循环，凭什么让 AI 从"能聊天"变成"能干活"？》

**来源**：用户输入文章（约 21 分钟阅读）
**新增页面**：
- concepts/agent-loop.md
- concepts/react-pattern.md
- comparisons/chatbot-vs-copilot-vs-agent.md
**更新页面**：
- index.md：补充 2 个概念入口 + 1 个对比入口
- concepts/harness-engineering.md：补充 agent-loop / react-pattern 交叉引用
- products/learn-claude-code.md：补充 agent-loop / react-pattern 交叉引用
**新增交叉引用**：
- agent-loop ↔ react-pattern/harness-engineering/mcp/subagent/learn-claude-code/claude-code-harness-analysis/chatbot-vs-copilot-vs-agent
- react-pattern ↔ agent-loop/harness-engineering/learn-claude-code/chatbot-vs-copilot-vs-agent
- chatbot-vs-copilot-vs-agent ↔ agent-loop/react-pattern/harness-engineering/learn-claude-code

## 2026-04-15: 收录《做 Agent 开发，有些大模型本身的底层机制，你不得不了解》

**来源**：用户输入文章（约 23 分钟阅读）
**新增页面**：
- concepts/tokenization.md
- concepts/autoregressive-generation.md
- concepts/kv-cache.md
- concepts/constrained-decoding.md
**更新页面**：
- index.md：补充 4 个概念入口
- concepts/agent-loop.md：补充与底层机制概念页的关联
- concepts/harness-engineering.md：补充与底层机制概念页的关联
- products/claude-code-harness-analysis.md：补充与底层机制概念页的关联
**新增交叉引用**：
- tokenization ↔ autoregressive-generation/kv-cache/constrained-decoding/agent-loop/harness-engineering/claude-code-harness-analysis
- autoregressive-generation ↔ tokenization/constrained-decoding/agent-loop/react-pattern/claude-code-harness-analysis
- kv-cache ↔ tokenization/agent-loop/harness-engineering/autoregressive-generation/claude-code-harness-analysis
- constrained-decoding ↔ autoregressive-generation/tokenization/agent-loop/harness-engineering/claude-code-harness-analysis

## 2026-04-15: 收录《浅谈 Agent Memory》

**来源**：https://mp.weixin.qq.com/s/8j6dX0yFAudjmmExmxB5MQ （浮之静，作者署名 lencx，微信公众号，2026-04-15，CDP 抓取）
**新增页面**：
- concepts/agent-memory.md — Agent Memory 的上位问题框架（认知分层 / 生命周期 / Raw vs Derived / 遗忘 / 治理 / 技能化）
**更新页面**：
- index.md：补充 1 个新概念入口（agent-memory）
- concepts/rag-knowledge-base.md：补充 “RAG 不是完整 Memory” 的边界说明与交叉引用
- concepts/layered-memory.md：补充与 agent-memory 的上位关联及参考来源
- concepts/skill-system.md：补充 Skills 作为程序性记忆的上位关联及参考来源
- concepts/self-evolution.md：补充与 agent-memory 的交叉引用及参考来源
- concepts/hermes-agent.md：补充与 agent-memory 的交叉引用
**新增交叉引用**：
- agent-memory ↔ layered-memory/skill-system/self-evolution/rag-knowledge-base/hermes-agent/agent-teams/harness-engineering
- rag-knowledge-base ↔ agent-memory
- layered-memory ↔ agent-memory
- skill-system ↔ agent-memory
- self-evolution ↔ agent-memory
- hermes-agent ↔ agent-memory
**审计备注**：
- 本文更适合作为“Agent Memory 总论”沉淀到 concepts，而不是机械按 Hermes / OpenClaw 某个具体实现页补丁式更新
- 页面中的具体论文与项目名主要作为问题框架的参考来源保留；核心沉淀是“记忆不是存档，而是时间中的状态治理”

## 2026-04-16: 收录 Claude Agent SDK 官方文档

**来源**：Anthropic 官方文档（https://code.claude.com/docs/en/agent-sdk/overview；同时查阅 `llms.txt`、migration guide、Claude Code features in the SDK）
**新增页面**：
- products/claude-agent-sdk.md — Anthropic 官方 Agent SDK，复用 Claude Code 的工具、agent loop、上下文管理与文件系统配置能力
**更新页面**：
- index.md：补充 1 个产品入口（claude-agent-sdk）
- concepts/agent-loop.md：补充 Claude Agent SDK 交叉引用与官方来源
- concepts/subagent.md：补充 Claude Agent SDK 交叉引用
- concepts/mcp.md：补充 Claude Agent SDK 交叉引用
- concepts/claude-code-skills.md：补充 SDK 通过 `settingSources` / `Skill` 复用 skills 的说明与官方来源
- products/learn-claude-code.md：补充与 Claude Agent SDK 的关系
- concepts/claude-to-im.md：补充其开发者 SDK 基于 Agent SDK 的关系
**新增交叉引用**：
- claude-agent-sdk ↔ agent-loop/subagent/mcp/claude-code-skills/learn-claude-code/everything-claude-code/claude-to-im

## 2026-04-17: 收录《Agent 时代，工程师最值钱的能力是说“不”》

**来源**：用户提供截图文章《Agent 时代，工程师最值钱的能力是说“不”》（手动 OCR 整理）
**新增页面**：
- concepts/engineering-sense.md — Agent 时代工程判断力的上位概念：排序、克制与明确说“不”的能力
- concepts/token-efficiency.md — 同等质量下用更少 token 完成任务的能力，是 Agent 系统规模化的核心约束
- patterns/benchmark-first-agent-development.md — 先搭 benchmark 再谈功能和优化的 Agent 开发模式
- patterns/prompt-as-system-design.md — prompt 作为系统设计承载物，而不只是下命令文本
- patterns/repo-native-expert-routing.md — repo 内知识作为唯一事实源，配合结构化路由表激活专家 Agent
**更新页面**：
- index.md：补充 2 个新概念入口与 3 个新模式入口
- concepts/harness-engineering.md：补充“harness 不是新瓶装出的新学问”视角，以及与 benchmark / prompt / expert routing 的交叉引用
- concepts/kv-cache.md：补充 Agent 请求模式如何破坏 prefix / KV cache 复用，以及与 token-efficiency 的关联
- concepts/multi-agent-architecture.md：补充 repo-native expert routing 的实践视角及关联页面
**新增交叉引用**：
- engineering-sense ↔ benchmark-first-agent-development/prompt-as-system-design/token-efficiency/harness-engineering/multi-agent-architecture/kv-cache
- token-efficiency ↔ tokenization/kv-cache/harness-engineering/benchmark-first-agent-development/prompt-as-system-design
- benchmark-first-agent-development ↔ engineering-sense/token-efficiency/prompt-as-system-design/harness-engineering
- prompt-as-system-design ↔ engineering-sense/benchmark-first-agent-development/harness-engineering/multi-agent-architecture
- repo-native-expert-routing ↔ multi-agent-architecture/subagent/supervisor-worker/harness-engineering
