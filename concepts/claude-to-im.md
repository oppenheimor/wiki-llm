# Claude-to-IM

> 将 Claude Code 远程连接到飞书、Discord、Telegram 等 IM 平台的开源工具集，包含用户友好的 Skill 和面向开发者的 SDK 两个项目。

## 核心能力

### Claude-to-IM-skill（面向终端用户）
安装后运行 `/claude-to-im setup`，Claude 会通过交互式引导逐步收集 token，并附带详细获取说明。无须编写代码。

- **三大 IM 平台**：Telegram、Discord、飞书，可任意组合启用
- **交互式配置**：Claude 引导式向导，无需手动操作配置
- **权限控制**：工具调用需在聊天中通过内联按钮明确批准
- **流式预览**：实时查看 Claude 输出（Telegram 和 Discord）
- **会话持久化**：守护进程重启后对话保留
- **密钥保护**：token 以 `chmod 600` 存储，日志自动脱敏

### Claude-to-IM SDK（面向开发者）
面向基于 Agent SDK 开发的第三方产品，快速接入多个 IM 远程控制。

- **多平台适配器**：Telegram（长轮询）、Discord（Gateway WebSocket）、飞书（WSClient）
- **流式预览**：通过消息编辑实现实时响应草稿
- **权限管理**：内联按钮审批 Claude Code 工具（允许 / 拒绝 / 本次会话允许）
- **会话绑定**：每个 IM 聊天映射到一个持久化会话，支持工作目录和模型配置
- **Markdown 渲染**：平台原生格式化（Telegram HTML、Discord Markdown、飞书富文本卡片）
- **可靠投递**：分块、指数退避重试、HTML 降级、消息去重
- **安全机制**：输入验证、令牌桶速率限制（每聊 20 条/分钟）、用户白名单、完整审计日志
- **宿主无关**：4 个 DI 接口抽象（不绑定数据库、LLM 客户端、框架）

## 技术亮点

- **多轮校验引导**：首次配置时 Claude 直接告诉你该点哪，门槛极低
- **无会话劫持**：每个 IM 对话绑定独立会话，权限边界清晰
- **流式响应**：Claude 输出实时同步到 IM，对话体验接近本地
- **SDK 插件式架构**：适配器模式，支持接入新的 IM 平台而不改核心代码

## 使用场景

- 外出时通过手机飞书远程操控本地 Claude Code
- 团队成员在 Discord 频道中调用共享的 Claude Code 实例
- 将 Claude Code 作为 Bot 接入现有 IM 工作流

## 安装方式

```bash
npx skills add op7418/Claude-to-IM-skill
```

## 关联页面

- [[concepts/claude-code-routines]] — 同作者的 Claude Code 远程自动化能力
- [[concepts/mcp]] — 类似的外部服务集成协议
- [[products/claude-agent-sdk]] — 面向开发者的 Claude-to-IM SDK 基于 Agent SDK 开发

## 参考来源

- 微信文章：https://mp.weixin.qq.com/s/bChoiIfApjg514alL0-y2Q
- Claude-to-IM-skill 仓库：https://github.com/op7418/Claude-to-IM-skill
- Claude-to-IM SDK 仓库：https://github.com/op7418/Claude-to-IM
