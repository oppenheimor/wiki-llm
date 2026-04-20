# Claude Code Harness 源码分析

> 基于 2026-03-31 意外泄露的 TypeScript 源码快照（1,900 文件、512,000 行），对 Claude Code 工业级 Agent Harness 架构的系统性逆向工程分析。

## 核心洞察

> **The model is the agent. The code is the harness.**
>
> 模型是智能体，代码是 Harness。Claude Code 不试图通过复杂的规则引擎或决策树模拟智能，而是将全部工程精力投入到为模型提供一个清晰、丰富、安全的操作环境。

## 整体架构

```
Claude Code = 单循环 + Harness
```

| 顶层目录 | Harness 角色 | 职责 |
|---|---|---|
| `src/tools/` | Agent 的双手 | 约 40 个原子工具（文件 I/O、Shell、LSP、MCP 等） |
| `src/commands/` | 用户指令接口 | 约 50 个斜杠命令 |
| `src/services/` | 外部服务集成 | API 客户端、MCP 协议、OAuth、LSP 集成 |
| `src/coordinator/` | 多智能体协调 | Sub-agent 编排、Team 管理 |
| `src/skills/` | 按需知识加载 | 渐进式披露的技能系统 |
| `src/bridge/` | IDE 桥接层 | VS Code、JetBrains ↔ CLI 双向通信 |
| `src/hooks/` | 权限与生命周期 | 工具权限校验、会话管理 |
| `src/plugins/` | 插件扩展 | 第三方插件加载 |
| `src/components/` | 终端 UI | 140+ React+Ink 组件 |
| `src/memdir/` | 持久记忆 | 跨会话记忆存储 |
| `src/tasks/` | 任务系统 | 带依赖图的任务管理 |
| `src/state/` | 状态管理 | 全局应用状态 |

## npm 分发形态补充

除了源码层的 Harness 结构，Claude Code 在交付层也采用了一个很典型的工程切分：npm 主包只承担 wrapper 与安装逻辑，真正的可执行文件按平台拆到 `optionalDependencies`，如 `@anthropic-ai/claude-code-darwin-arm64`。

这意味着“`claude` 命令存在”不等于“真实二进制存在”。当第三方镜像缺失某个平台包，或 optional dependency 下载失败时，用户会得到一个能被找到但启动时报 `native binary not installed` 的半安装状态。这个现象本质上属于分发层问题，而不是 agent loop、权限或工具执行层问题。

## 核心文件

| 文件 | 规模 | 职责 |
|---|---|---|
| `QueryEngine.ts` | ~46K 行 | LLM 查询引擎：流式响应、工具调用循环、思考模式、重试逻辑、Token 计数 |
| `Tool.ts` | ~29K 行 | 工具基础类型定义：Zod v4 Schema、权限模型、进度状态 |
| `commands.ts` | ~25K 行 | 斜杠命令注册与执行 |
| `main.tsx` | 入口 | Commander.js 解析 + React/Ink 初始化 + 并行预取 |

## 工具系统设计原则

### 三原则
- **原子性**：每个工具只做一件事（如 `FileReadTool` 只读、`FileEditTool` 只改），职责单一
- **可组合性**：工具输出自然成为下一个工具的输入（如 Grep → Read → Edit）
- **自我描述性**：每个工具通过 Zod v4 Schema 精确描述输入输出，允许 `ToolSearchTool` 实现延迟工具发现（节省上下文窗口）

### 单次工具调用不是“模型说了就执行”

从工具工程角度看，Claude Code 的关键价值不只是拥有很多工具，而是把一次调用拆成多层处理：schema 验证、业务校验、输入补全、前置 Hook、权限检查、真实执行、结果截断与错误整形。这里的错误返回不是传统给开发者看的底层错误码，而是给模型看的“可纠正反馈”，这直接影响自修复效率。

### 结果预算是上下文工程的一部分

工具输出过长时，Claude Code 不会无脑把完整结果塞回对话历史，而是用结果预算和落盘引用保护上下文窗口。这说明工具系统不仅是执行层，也是 token 经济和缓存命中率管理的一部分。

用户输入文章《Claude Code 上下文管理机制》补充了更细的阈值与布局视角：单个工具结果超过 5 万字符、或一轮并行工具结果合计超过 20 万字符时，Claude Code 会把完整输出持久化到磁盘，只在上下文里保留短预览与文件路径。这让“工具结果落盘”从经验描述上升为明确的运行时策略。

### 工具清单（按层次分类）

| 层次 | 工具 | 说明 |
|---|---|---|
| 行动层 | BashTool, FileWriteTool, FileEditTool, NotebookEditTool | 直接操作环境 |
| 感知层 | FileReadTool, GlobTool, GrepTool, WebFetchTool, WebSearchTool | 获取信息 |
| 协调层 | AgentTool, TaskCreate/UpdateTool, SendMessageTool, TeamCreate/DeleteTool | 多智能体协作 |
| 知识层 | SkillTool | 按需加载技能 |
| 认知层 | EnterPlanModeTool, ExitPlanModeTool | 规划模式切换 |
| 隔离层 | EnterWorktreeTool, ExitWorktreeTool | Git Worktree 文件系统隔离 |
| 元层 | ToolSearchTool, SyntheticOutputTool | 延迟发现、结构化输出 |
| 调度层 | CronCreateTool, RemoteTriggerTool, SleepTool | 定时/远程触发 |

## 上下文三层压缩策略

1. **子智能体独立上下文**：Sub-agent 的 `messages[]` 不污染主会话，只返回结果摘要
2. **自动对话压缩（compact service）**：接近窗口限制时将早期对话压缩为摘要，保留关键决策
3. **持久化（memdir + tasks）**：任务状态写入磁盘，`/resume` 可跨会话恢复

### Prompt Cache 是压缩策略的隐含上位约束
《Claude Code 上下文管理机制》指出，Claude Code 会把 system prompt 静态部分与工具定义组织成可缓存前缀，再把工作目录、日期、`CLAUDE.md`、消息历史和 attachments 放入动态区。这样设计的关键不是“分层好看”，而是避免压缩与动态更新打烂缓存前缀。

## 多智能体协调：六种架构模式

| 模式 | 适用场景 | 通信方式 |
|---|---|---|
| Pipeline | 顺序依赖（设计→前端→后端→测试） | 上一步输出作下一步输入 |
| Fan-out/Fan-in | 并行独立（多维度代码审查） | 分发后聚合 |
| Expert Pool | 专业任务动态选择 | 根据任务类型分发 |
| Producer-Reviewer | 生成后验证 | 生产者↔审核者交替 |
| Supervisor | 中心化动态调度 | Supervisor 统一调度 |
| Hierarchical Delegation | 复杂任务递归拆分 | 树状层级 |

## 权限系统

| 模式 | 行为 |
|---|---|
| `default` | 每次工具调用前审批 |
| `plan` | 规划阶段只读，执行时审批 |
| `auto` | 低风险自动批准，高风险仍审批 |
| `bypassPermissions` | 跳过所有检查（沙箱/测试） |

## 性能优化技术

- **并行预取**：启动时并行加载 CLI 解析、配置读取、连接器初始化
- **动态 `import()`**：重量级模块（OpenTelemetry、gRPC）延迟加载
- **死代码消除**：通过 Bun `bun:bundle` 特性标志在编译时剪除未启用功能
- **特性门控**：PROACTIVE、KAIROS、BRIDGE_MODE、DAEMON、VOICE_MODE 等可选子系统

## 技术栈

| 类别 | 选型 | 意义 |
|---|---|---|
| 运行时 | Bun | 高性能 JS/TS 运行时 |
| 语言 | TypeScript (strict) | 类型安全 |
| 终端 UI | React + Ink | 用 React 组件构建 TUI |
| CLI 解析 | Commander.js | 命令行解析 |
| Schema 验证 | Zod v4 | 运行时类型安全 |
| 代码搜索 | ripgrep | 极速正则搜索 |
| 外部协议 | MCP SDK, LSP | 标准化工具集成 |
| API | Anthropic SDK | 与 Claude 模型通信 |
| 遥测 | OpenTelemetry + gRPC | 可观测性 |
| 特性标志 | GrowthBook | A/B 测试与渐进发布 |

## 关联页面

- [[concepts/harness-engineering]] — 本分析所基于的核心概念
- [[concepts/tokenization]] — 长上下文和 Token 计数的底层计量单位
- [[concepts/autoregressive-generation]] — 流式响应与工具参数碎片化输出的生成机制
- [[concepts/kv-cache]] — 长上下文下延迟与成本优化的关键缓存机制
- [[concepts/prompt-cache]] — 请求前缀缓存对上下文布局与压缩策略形成直接约束
- [[concepts/constrained-decoding]] — 结构化输出与工具调用可靠性的解码约束基础
- [[concepts/agent-teams]] — 多智能体协调机制
- [[concepts/subagent]] — 子智能体生成机制
- [[concepts/tool-execution-pipeline]] — 单次工具调用的分层处理模式
- [[patterns/agent-four-layers-2026]] — 2026 年 Agent 生态四层框架
- [[patterns/npm-mirror-optional-native-package-gap]] — npm 镜像缺包导致 wrapper 存在但原生二进制缺失的排障模式
- [[products/everything-claude-code]] — 154K stars 的配置体系
- [[products/learn-claude-code]] — Harness 工程 0→1 教学项目
- [[concepts/claude-code-routines]] — 云端自动化运行

## 参考来源

- 微信文章《从Harness角度对Claude Code源码深度解读》：https://www.51cto.com/article/839733.html
- 源码快照来源：https://github.com/instructkr/claude-code（原始 npm 发布包 source map 泄露）
- 教学项目：https://github.com/shareAI-lab/learn-claude-code
- 用户输入文章《一次工具调用背后经历了什么？以 Claude Code 为例展开聊聊》（2026-04-17 收录）
- 用户输入文章《Claude Code 上下文管理机制》（2026-04-17 收录）
- 本机安装排障记录（2026-04-18）：`@anthropic-ai/claude-code@2.1.114` 主包存在，但 `@anthropic-ai/claude-code-darwin-arm64@2.1.114` 在 `registry.npmmirror.com` 缺失，导致 `claude native binary not installed`
