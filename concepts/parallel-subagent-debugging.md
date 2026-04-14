# Parallel Subagent Debugging（并行 Subagent 调试）

> 将大量独立 bug 或缺陷一次性喂给 AI，由 AI 自动分配多个 subagent 并行修复，最后统一截图校验结果的开发模式。

## 核心思路

- **批量输入**：10-20 个 bug 一次性提交，而非逐个处理
- **AI 自动分诊**：AI 判断每个 bug 的性质，决定修复优先级和方式
- **并行执行**：多个 subagent 同时工作，互不阻塞
- **统一验收**：人工截图确认是否还原正常

## 工作效率

作者描述 Harness 工程中，10-20 分钟的构建配合 10-20 个 bug 的并行修复，"AI 拉磨时人可以吹水或看其他内容"——本质是将等待时间变为并行产出时间。

## 适用条件

- Bug 之间相互独立，无强依赖关系
- 有快速验收手段（截图、自动化测试）
- AI 模型对代码库上下文理解充分
- 构建/CI 周期明显长于人工操作时间

## 关联页面

- [[concepts/vibercoding]] — AI 主导编码
- [[concepts/hermes-agent]] — Hermes Agent 支持多 subagent 并行处理
- [[concepts/self-evolution]] — 智能体自我评估修复效果

## 参考文档

- 《我是这么用 AI 的》：微信公众号（2026-04-13）
