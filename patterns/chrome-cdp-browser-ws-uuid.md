---
name: Chrome CDP Browser WS UUID 陷阱
description: Chrome 通过 chrome://inspect 勾选框启用调试时，Browser 级 WebSocket 路径强制带 UUID，裸路径握手成功后会被立刻关闭
type: pattern
---

# Chrome CDP Browser WebSocket UUID 陷阱

> Chrome 启用远程调试有两种方式，二者对 Browser 级 WebSocket 路径的要求不同。写死裸路径 `/devtools/browser` 的 CDP 客户端，在其中一种方式下会出现"握手成功立刻断开"的循环。

## 现象

CDP Proxy 日志反复循环：
```
[CDP Proxy] 从 DevToolsActivePort 发现端口: 9222
[CDP Proxy] 已连接 Chrome (端口 9222)
[CDP Proxy] 连接断开
[CDP Proxy] 从 DevToolsActivePort 发现端口: 9222
[CDP Proxy] 已连接 Chrome (端口 9222)
[CDP Proxy] 连接断开
...
```

表现特征：
- `lsof -i :9222` 显示 Chrome 进程在 LISTEN 状态，端口正常开放
- `/health` 返回 `{"connected":null}` 或 `false`
- **时灵时不灵**：同样代码，有时能连上有时不行，Cmd+Q 重启 Chrome 后结果会变
- `onopen` 事件正常触发（日志里"已连接"这一步是真的成功了），紧接着 `onclose` 立刻触发

## 根因：两种启用方式的差异

Chrome 启用远程调试有两条路径，行为不等价：

| 启用方式 | HTTP 发现端点 | Browser WS 路径要求 |
|---|---|---|
| 命令行 `--remote-debugging-port=9222` | `/json/version`、`/json/list` 可访问 | 裸路径 `/devtools/browser` 可用 ✅ |
| `chrome://inspect` 勾选 "Allow remote debugging for this browser instance" | **全部 404** | **必须带 UUID**，如 `/devtools/browser/c57b3c52-f529-4a68-ab50-cf97ec141212` ❌ |

勾选框模式下，Chrome 接受 WebSocket 握手（`onopen` 触发），随后校验路径发现没 UUID，立刻关闭连接（`onclose` 触发）。客户端拿到的信号是："连接成功了，但是瞬间就断了"——这就是循环重连的来源。

**"时灵时不灵"的真相**：用户每次重启 Chrome 的启动方式可能不同。命令行启动和勾选框启动在本机都留下监听 9222 的 Chrome 进程，TCP 探测和 HTTP 端点可用性却不同，结果自然不一样。

## 排查思路

当看到"握手成功→立刻断开"的循环时，排查顺序：

1. **先确认不是端口问题**：`lsof -i :9222` 如果端口在监听，就不是 Chrome 没启动或防火墙挡了
2. **探测 HTTP 发现端点**：`curl http://127.0.0.1:9222/json/version`
   - 返回正常 JSON → 命令行启动模式，问题在别处
   - **返回 404** → 勾选框模式，立刻怀疑 WS 路径
3. **读 DevToolsActivePort 文件**：macOS 在 `~/Library/Application Support/Google/Chrome/DevToolsActivePort`
   ```
   9222
   /devtools/browser/c57b3c52-f529-4a68-ab50-cf97ec141212
   ```
   - 第一行是端口号
   - **第二行是权威的 Browser WebSocket 路径**，由 Chrome 自己写入
4. **对比客户端代码**：如果客户端硬编码了裸路径 `ws://host:port/devtools/browser`，就是根因

关键洞察：**`onopen` 触发不等于连接可用**。CDP 协议层的路径校验发生在 WebSocket 握手之后，需要用 `onclose` 的紧接触发作为信号。

## 解决方案

**不硬编码 WS 路径，从 `DevToolsActivePort` 文件第二行读取**。这个文件由 Chrome 自己维护，是权威来源：

```js
// 读文件时同时捕获端口和路径
const content = fs.readFileSync(devToolsActivePortPath, 'utf-8').trim();
const lines = content.split('\n');
const port = parseInt(lines[0]);
const wsPath = (lines[1] && lines[1].startsWith('/devtools/browser'))
  ? lines[1]
  : '/devtools/browser';  // 裸路径作为兜底（命令行模式下有效）

const wsUrl = `ws://127.0.0.1:${port}${wsPath}`;
```

配合两个注意点：
- **断连时重置路径缓存**：Chrome 重启后 UUID 会变，`onclose` 里把 `wsPath` 也清掉，下次连接重新读文件
- **裸路径保留作为 fallback**：兼容命令行启动方式，这样代码在两种模式下都能工作

## 经验沉淀

- 硬编码任何"看起来固定"的协议路径都有风险，Chrome 这类复杂系统尤其容易在新版本加入安全约束
- 当产品提供了自描述文件（`DevToolsActivePort`、`/json/version` 等），优先从自描述源读取，而不是根据文档"应该是什么样"去拼
- WebSocket 握手成功 ≠ 应用层连接可用。应用层协议可能在握手后才做路径/鉴权校验
- "时灵时不灵"几乎总是有确定性的状态差异，不要归因于"随机"。把每次成功和失败的环境变量都列出来对照

## 参考来源

- 本机实际排查案例（2026-04-15）
- 修复位置：`~/.claude/skills/web-access/scripts/cdp-proxy.mjs` 的 `discoverChromePort` 与 `getWebSocketUrl`
- Chromium 源码中 DevToolsActivePort 写入逻辑：`content/browser/devtools/devtools_http_handler.cc`

## 关联页面

- [[concepts/claude-code-skills]] — web-access 是 Claude Code skill 的典型应用
