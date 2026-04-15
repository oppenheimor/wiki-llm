# Hermes Agent

> Nous Research推出的自进化本地AI智能体，能通过使用不断自我提升，而非仅执行任务和存储记忆。

## 核心能力

- **自我进化**：每次交互评估效果，将有效工作流抽象为可复用技能，从"记住事实"进化到"记住方法"
- **分层记忆体系**：核心持久记忆（MEMORY.md/USER.md）→ 会话历史（SQLite+FTS5）→ Honcho长期画像 → 程序化技能层
- **跨平台部署**：本地终端、VPS、Docker、SSH、无服务器架构均可运行
- **模型无关**：支持 OpenAI、OpenRouter、Kimi、GLM 等任何兼容 OpenAI API 的端点
- **定时自动化**：内置 cron 计划任务系统，支持自然语言指定定期任务
- **并行任务处理**：可为调研和多线程任务生成隔离的 subagent 并行处理，最后汇总结果

## 技术架构

Hermes 将 AI Agent 循环本身定义为**核心同步编排引擎**，围绕它集成：
- 网关、定时任务调度器
- 工具运行时
- ACP（Agent Communication Protocol）
- 基于 SQLite 的会话持久化
- 强化学习（RL）环境

与 OpenClaw 的"中心化控制器"思路不同，Hermes 强调"执行—学习—改进"的自我进化闭环。

## 安全设计

内置**五层纵深防御模型**：
1. 用户授权
2. 危险命令审批
3. 容器隔离
4. MCP 凭证过滤
5. 上下文文件扫描

此外还有 SSRF 防护、网站黑名单、环境变量过滤、消息用户配对及预执行扫描。

## 安装方式

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

支持从 OpenClaw 一键迁移（自动检测 `~/.openclaw` 配置并导入记忆与技能）。

公众号文章补充了一个对实际落地很重要的细节：Hermes 虽然安装门槛比 OpenClaw 更低，也支持从 OpenClaw 通过 `hermes claw migrate` 一键搬迁配置、记忆、API Key 和 Skills，但如果想让它真正成为“随时叫随时到”的助理，仍然需要一台 7×24 在线的宿主机。

## 运行前提

Hermes 适合部署在本地常开设备、VPS、Docker 或 SSH 可达的远程主机上。它的自我进化、定时自动化和远程使用价值，只有在宿主机稳定在线时才会持续释放；否则再强的 Agent 也只是“你开机时才出现的工具”。

## 关联页面

- [[products/everything-claude-code]] — Anthropic 黑客松冠军的 Claude Code 配置体系，与 Hermes Agent 有相似的"把方法论变成可复用结构"的设计思想
- [[concepts/openclaw]]
- [[concepts/self-evolution]]
- [[concepts/layered-memory]]
- [[concepts/skill-system]]
- [[patterns/agent-always-on-host]] — 自托管 Agent 持续可用性的基础设施前提

## 参考文档

- Hermes Agent 架构文档：https://hermes-agent.nousresearch.com/docs/developer-guide/architecture
- Hermes Agent vs OpenClaw 解析：微信公众号文章（2026-04-14）
- 微信公众号：龙虾退热后，爱马仕来了（2026-04-15）
