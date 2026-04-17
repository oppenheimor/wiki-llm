# gstack

> 面向编码 Agent 的执行型技能工具箱，通过 `/browse`、`/qa`、`/ship`、`/canary` 等 slash commands 封装浏览器、测试、发布与护栏动作。

## 核心能力
- **浏览器与 QA 执行面**：提供 `/browse`、`/qa`、`/design-review` 等真实页面验证能力。
- **发布流水线封装**：用 `/ship`、`/land-and-deploy`、`/canary` 串起测试、PR、部署与回归监控。
- **多宿主安装**：支持 Claude Code、Codex CLI、OpenCode、Cursor、Hermes 等多个 Agent 宿主。
- **团队模式分发**：可通过 `--team` 和仓库 bootstrap 把技能版本分发给协作成员。

## 技术亮点
### 它代表的是“执行面 skill 包”，不是另一套方法论
与强调流程约束的 Superpowers 不同，gstack 更偏向把浏览器、QA、发布、回滚、监控等高频动作封装成可重复调用的入口。它回答的是“具体怎么干”，而不是“应不应该先想清楚”。

### Slash command 是它的产品边界
gstack 把一组角色化能力收敛成固定的 slash commands，使浏览器验证、端到端测试、发布和护栏拥有统一入口。这样可以减少“同一能力在多个插件里重名抢匹配”的混乱。

## 使用场景
- 需要把浏览器验证、QA、发布与监控纳入编码 Agent 工作流
- 前端或全栈项目中，希望 Agent 直接操作真实页面和上线链路
- 团队想统一一套执行型 slash commands，而不是各自拼装工具集

## 关联页面
- [[concepts/claude-code-skills]]
- [[concepts/harness-engineering]]
- [[patterns/tool-aware-streaming-ui]]
- [[products/superpowers]]

## 参考来源
- GitHub README：https://github.com/garrytan/gstack（2026-04-17 查阅）
- 用户输入文章《实战篇: Claude Code + superpowers + gstack 开发流程实录，可直接复制使用，一篇文章讲清楚！》（2026-04-17 收录）
