# Claude Code Routines

> Claude Code 的自动化运行功能，允许用户配置一次 prompt 后让 AI 在云端自动执行任务，支持定时触发、API 触发、GitHub 事件触发三种方式。

## 核心能力

- **三种触发方式**：定时触发、API 触发、GitHub 事件触发
- **云端运行**：在 Anthropic 云端基础设施上运行，不依赖本地设备
- **连接器集成**：可接入 Slack、Linear、Google Drive 等外部服务
- **全面开放**：Pro/Max/Team/Enterprise 用户均可使用（20 美元 Pro 档也可使用）

## 触发方式详解

### 1. 定时触发
给 Claude 设个闹钟。每小时、每天、每周，或者自定义 cron 表达式。

典型场景：每天凌晨 2 点去 Linear 里捞最新的 bug，尝试修复，然后开个 draft PR。你醒来的时候，PR 已经在那了。

### 2. API 触发
每个 Routine 都有自己的 HTTP 端点。监控系统报警了？直接把告警 payload POST 过去，Claude 会自己去查日志、关联最近的 commit、开个修复 PR。

```bash
curl -X POST https://api.anthropic.com/v1/claude_code/routines/trig_xxx/fire \
  -H "Authorization: Bearer sk-ant-oat01-xxxxx" \
  -d '{"text": "Sentry alert SEN-4521 fired in prod."}'
```

### 3. GitHub 事件触发
支持 PR opened、push、issue created、release published 等十几种 GitHub 事件。

典型场景：只要有 PR 动了 /auth 目录下的文件，就自动做一次安全审查，把结果贴到 PR 评论里。

这三种触发方式可以叠加，同一个 Routine 既定时跑，又监听 PR，还能被 API 调用。

## 与 /schedule 的区别

如果你之前用过 Claude Code 的 /schedule 命令：

| 特性 | /schedule | Routines |
|------|-----------|---------|
| 运行位置 | 本地 | 云端 |
| 触发方式 | 定时 | 定时 + API + GitHub |
| 连接器 | 有限 | 完整接入 |

Routines 是 /schedule 的进化版，Claude 从「你喊它才动」变成了「它自己盯着，有事就动」。

## 典型使用场景

- **积压清理**：每天晚上扫一遍 issue tracker，自动打标签、分配负责人，第二天早上团队直接看结果
- **告警分诊**：监控系统触发 API 端点，Claude 拿到告警后自己去查，关联代码变更，开修复 PR。on-call 的人只需要 review 不用从零开始排查
- **文档同步**：每周扫一遍已合并的 PR，找到改了 API 但没更新文档的地方，自动开 PR 补上
- **代码审查**：PR opened 时运行团队自定义的安全审查 checklist

## 创建方式

1. **网页**：在 claude.ai/code/routines 上创建，最完整
2. **CLI**：用 /schedule 命令创建（目前只支持定时触发）
3. **Desktop**：点 New task → New remote task

## 重要限制

- 目前处于 Research Preview 阶段
- 每个账号每天有 Routine 运行次数上限
- GitHub 事件触发有每小时的频率上限
- 行为、限制、API 接口都可能变化

## 关联页面

- [[products/everything-claude-code]] — Claude Code 四层配置体系
- [[concepts/claude-code-rules]] — 配置规则层
- [[concepts/claude-code-skills]] — 配置技能层
- [[concepts/claude-code-hooks]] — 配置钩子层
- [[concepts/claude-code-agents]] — 配置代理层

## 参考来源

- 微信公众号：刚刚，Claude Code 推出 Routines，让 AI 自动帮你值夜班（2026-04-15）
- 官方文档：https://code.claude.com/docs/en/routines
- 产品页面：https://claude.com/product/claude-code