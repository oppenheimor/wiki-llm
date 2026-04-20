# NPM 镜像缺失 Optional Native Package 排障模式

> 当 CLI 采用“JS wrapper + 平台原生二进制 optionalDependencies”分发时，镜像源缺包会导致主包安装成功、启动却报 native binary missing 的半安装状态。

## 问题场景

这类问题常出现在通过 npm 安装的本地 CLI 工具上，尤其是产品把启动入口做成一个很小的 JavaScript wrapper，再把真正的可执行文件拆成按平台分发的 optional dependency。

表面现象通常很迷惑：
- `npm i -g <pkg>` 成功，`which <cmd>` 也能找到命令
- 启动时报 `native binary not installed`、`Could not find native binary package`、`postinstall did not run` 一类错误
- 用户容易误判成 PATH、权限、Node 版本或 postinstall 脚本本身损坏

## 解决方案

排查顺序应优先确认“主包是否装上”与“平台包是否缺失”是两回事，而不是一上来重装：

1. 先复现真实错误，记录 CLI wrapper 给出的原始报错。
2. 检查当前平台与架构，确认理论上应该安装哪个 optional package。
3. 打开主包的 `package.json`，确认其 `optionalDependencies` 列表与 `postinstall` 行为。
4. 检查 npm 当前使用的 registry，尤其是是否指向第三方镜像。
5. 单独查询缺失的平台包在当前 registry 是否存在；若镜像返回 404，再去官方 registry 复核。
6. 用官方 registry 补装缺失的平台包，再重新执行主包的 `postinstall` 或安装脚本。

这套顺序的关键价值在于：它能把“CLI 损坏”收敛为“镜像源内容不完整”这一类分发问题，避免无效重装。

## 权衡取舍

- 依赖第三方 npm 镜像可以换取下载速度，但代价是平台特定包、可选依赖和最新版本更容易出现同步不完整。
- CLI 采用 wrapper + native binary 的分发方式，启动性能和跨平台交付更好，但排障时必须意识到“命令存在”并不代表“真实二进制存在”。
- 直接切回官方 registry 最稳，但如果团队有统一镜像策略，至少应对这类平台包保留官方源兜底。

## 实战案例：Claude Code 安装后启动报错

2026-04-18 在本机排查 Claude Code 时，真实现象是：
- `claude` 命令存在，来自 `~/.nvm/versions/node/v24.14.0/bin/claude`
- 启动报错：`claude native binary not installed`
- 主包 `@anthropic-ai/claude-code@2.1.114` 已安装
- 机器平台是 `darwin arm64`

进一步检查发现：
- 主包的 `package.json` 将真实二进制拆到 `@anthropic-ai/claude-code-darwin-arm64` 等 `optionalDependencies`
- `~/.npmrc` 的默认源是 `https://registry.npmmirror.com/`
- 该镜像对 `@anthropic-ai/claude-code-darwin-arm64@2.1.114` 返回 404
- 官方 `https://registry.npmjs.org/` 上该版本存在

最终修复动作：

```bash
npm install -g @anthropic-ai/claude-code-darwin-arm64@2.1.114 --registry=https://registry.npmjs.org/
node ~/.nvm/versions/node/v24.14.0/lib/node_modules/@anthropic-ai/claude-code/install.cjs
claude --version
```

验证结果为 `2.1.114 (Claude Code)`，说明问题不在 Claude Code 主包本身，而在镜像源漏同步了平台原生包。

## 关联页面

- [[products/claude-code-harness-analysis]] — Claude Code 的 npm 分发形态里存在 wrapper 与平台原生包拆分
- [[concepts/tool-execution-pipeline]] — 错误信息应该能把失败收敛为可纠正反馈，而不是只暴露模糊症状
- [[concepts/harness-engineering]] — 工具、权限、错误整形与分发边界共同决定真实可运维性

## 参考来源

- 本机实测（2026-04-18）：`claude --version` 报错 `claude native binary not installed`
- 本机文件：`/Users/paulchess/.nvm/versions/node/v24.14.0/lib/node_modules/@anthropic-ai/claude-code/package.json`
- 本机文件：`/Users/paulchess/.npmrc`
- 本机命令：`npm view @anthropic-ai/claude-code-darwin-arm64 versions --json --registry=https://registry.npmjs.org/`
