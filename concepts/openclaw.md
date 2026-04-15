# OpenClaw

> 一个以工作区文件为核心、强调操作者完全掌控权的自托管本地AI智能体框架。原名 Clawdbot，由 macOS 知名开发者 **Peter Steinberger** 开源。核心理念是"主权 AI"——Agent 的一切状态都以纯文本存在用户自己的电脑上。

## 历史与收购

- 个人/周末项目起步，3 个月内 GitHub Star 数突破 20 万
- **2026 年初被 OpenAI 收购**——这成为"协议 vs 平台"讨论中被反复引用的案例：平台会被收购关停，只有开放协议下的经验才真正属于用户（见 [[concepts/gep-protocol]]）

## 核心设计理念

OpenClaw 将身份和行为封装进**基于文件的工作区**，使智能体可被检查、追踪和版本管理。智能体的个性与它所处的具体工作区绑定，而非全局抽象。从 Claude Code 的 `CLAUDE.md`（项目级："这个项目怎么做"）到 OpenClaw 的 `SOUL.md`（人级："你是谁"），记忆的粒度从项目迁移到了个体。

## 核心组件

- **Gateway（网关）**：长期运行的进程，作为控制中枢负责会话管理、路由、工具调用和状态维护
- **工作区文件**：
  - `SOUL.md` — 身份定义
  - `AGENTS.md` — 智能体行为
  - `USER.md` — 用户偏好
  - `MEMORY.md` — 记忆
  - `TOOLS.md` — 工具定义
  - `HEARTBEAT.md` — 主会话心跳感知
  - 技能文件、每日笔记
- **技能机制**：可复用、由人类编写的工作流指令，按工作区、个人、共享或插件范围加载

## 内存机制

OpenClaw 的记忆基于 **Markdown 文件**，文件是事实的权威来源。与 Hermes 的动态分层记忆不同，OpenClaw 的记忆是显式的、基于文件的、可版本管理的。

## 安全特性

OpenClaw 假定操作者能够理解并承担委托工具权限带来的风险，是一个以操作者为核心、可深度加固的系统。安全加固更多依赖用户自身的运维方式，官方提供工具策略、沙箱隔离、权限控制等建议。

## 独特能力：GUI 自动化

除了 MCP、Skills、命令行工具这些"后台"能力，OpenClaw 还能像人一样操作图形界面——真的点按钮、填输入框、在不同 App 之间切换。例如你说"帮我在飞书上建一个项目空间，把这几个人拉进去"，它会真的打开飞书一步步操作。

**这解决的现实问题**：很多软件没有 API、也没接入 MCP，Agent 没法从后台连接它们。但只要它有界面，OpenClaw 就能操作。这是一条在 MCP 生态尚未覆盖的角落里的兜底路径。

## 心跳机制与主动工作

`HEARTBEAT.md` 文件 + 系统后台守护进程构成了 OpenClaw 的主动工作能力：
- 守护进程每隔一段时间"戳"一下 Agent
- Agent 醒来读 `HEARTBEAT.md` 看有没有定时任务
- 有就干，没有继续睡

典型用法：每天早上 9 点检查邮箱发摘要、每小时看一眼监控页面、聊天里说"一小时后提醒我开会"让 Agent 自己给自己设闹钟。

这把用户与 Agent 的关系从"你主动找 Agent 帮忙"转成了"Agent 主动替你盯着"，是 [[patterns/agent-four-layers-2026]] 第三层"主动工作"的典型实现。

## 优势

- 基础设施支持强大（NVIDIA、OpenAI 资源加持）
- 多平台消息接口完善
- 文件驱动身份系统：工作区持久、可版本控制
- 可深度定制和加固
- GUI 自动化补齐 MCP 覆盖盲区

## 关联页面

- [[concepts/hermes-agent]]
- [[concepts/skill-system]]
- [[concepts/mcp]]
- [[concepts/gep-protocol]]
- [[patterns/agent-four-layers-2026]]

## 参考文档

- OpenClaw GitHub：https://github.com/openclaw/openclaw
- 官方文档：https://docs.openclaw.ai/zh-CN
- Hermes Agent vs OpenClaw 解析：微信公众号文章（2026-04-14）
- 歸藏的AI工具箱《过了个年，AI 圈变天了？但没人告诉你为什么》（2026-02-25）
