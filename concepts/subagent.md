---
name: SubAgent（子智能体）
description: 主 Agent 临时派生的专门子进程，用 token 消耗换上下文清洁——"搜索的本质是压缩"
type: concept
---

# SubAgent（子智能体）

> 主 Agent 在执行任务过程中临时创建的专门子 Agent。子 Agent 完成子任务后把结果压缩成简短摘要交回来，然后消失。主 Agent 不需要知道子 Agent 具体怎么干的，只需要拿到结果。

## 解决的核心问题：上下文窗口污染

LLM 的上下文窗口是有限的。当主 Agent 需要做一个复杂任务（如调研技术方案、翻多个代码仓库、读大量文档），如果所有搜索过程和中间结果都塞进主 Agent 的上下文里：

- 上下文很快被撑满
- 一旦接近上限，主 Agent 的思考质量显著下降
- 长上下文注意力稀释，关键信息被淹没

SubAgent 的本质是给主 Agent 做**上下文外包**。

## 工作方式

以"调研技术方案"为例：

1. 主 Agent 收到任务，识别出需要翻几个仓库
2. 主 Agent 派出几个子 Agent，每个负责翻一个仓库
3. 每个子 Agent 独立消耗几万 token 做搜索和阅读
4. 子 Agent 最后只交回一两千 token 的**精华摘要**
5. 主 Agent 的上下文保持干净，思考质量不受影响
6. 子 Agent 使命完成，上下文整体蒸发

Anthropic 内部的说法：**"搜索的本质是压缩"**。SubAgent 就是在帮主 Agent 做压缩——它在自己的一次性上下文里消费大量信息，挤出几百字浓缩物返回。

## 成本与安全优化

- **更便宜的小模型**：探索类子任务会被自动分配给更便宜、更快的小模型（如 Claude Haiku），把贵的 Opus 留给主 Agent 做高阶判断
- **只读权限**：子 Agent 通常只拿到只读权限，避免误操作用户的文件
- **无状态**：子 Agent 结束时上下文整体蒸发，不会污染主 Agent 的后续思考

## 与 Agent Teams 的区别

SubAgent 是"一次性压缩工具"，[[concepts/agent-teams]] 是"持续协作的团队成员"。两者是 Multi-Agent 体系的两个不同原语：
- 需要"一次性翻一堆资料"→ SubAgent
- 需要"多人长期协作一个大项目"→ Agent Teams

## 参考来源

- 歸藏的AI工具箱《过了个年，AI 圈变天了？但没人告诉你为什么》（2026-02-25）
- Anthropic 关于 SubAgent 与搜索压缩的公开说法

## 关联页面

- [[patterns/agent-four-layers-2026]]
- [[concepts/agent-teams]]
- [[concepts/parallel-subagent-debugging]]
- [[concepts/claude-code-agents]]
