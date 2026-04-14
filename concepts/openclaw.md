# OpenClaw

> 一个以工作区文件为核心、强调操作者完全掌控权的自托管本地AI智能体框架。

## 核心设计理念

OpenClaw 将身份和行为封装进**基于文件的工作区**，使智能体可被检查、追踪和版本管理。智能体的个性与它所处的具体工作区绑定，而非全局抽象。

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

## 优势

- 基础设施支持强大（NVIDIA、OpenAI 资源加持）
- 多平台消息接口完善
- 文件驱动身份系统：工作区持久、可版本控制
- 可深度定制和加固

## 关联页面

- [[concepts/hermes-agent]]
- [[concepts/soul-md]]
- [[concepts/skill-system]]

## 参考文档

- OpenClaw GitHub：https://github.com/openclaw/openclaw
- Hermes Agent vs OpenClaw 解析：微信公众号文章（2026-04-14）
