# AgentShield

> 内置于 [[products/everything-claude-code]] 的 Claude Code 配置安全扫描工具，1282 项测试，102 条静态分析规则，扫描配置中的安全漏洞。

## 核心能力

- **1282 项测试**：覆盖广泛的安全测试场景
- **102 条静态分析规则**：自动化代码审查规则
- **一键扫描**：简单命令即可运行

## 扫描覆盖范围

AgentShield 检查 Claude Code 配置中的以下安全风险：

1. **密钥泄露风险**：检测配置中是否存在硬编码的密钥、token、凭证
2. **权限配置问题**：检查 MCP 配置的权限设置是否过于宽松
3. **注入风险**：识别可能导致指令注入的配置问题

## 使用场景

当你在 Claude Code 中接入了多个 MCP（Model Context Protocol）时，建议运行一次 AgentShield 扫描，确保：
- CLAUDE.md 中的信息不会泄露敏感内容
- MCP 配置的权限在合理范围内
- Hooks 中没有引入安全漏洞

## 使用方式

```bash
npx ecc-agentshield scan
```

## 关联页面

- [[products/everything-claude-code]] — AgentShield 所属的配置体系
- [[patterns/claude-code-config-layers]] — Claude Code 配置分层模式

## 参考来源

- 微信公众号：154K Star！Anthropic黑客松冠军的Claude Code配置大公开（2026-04-14）
