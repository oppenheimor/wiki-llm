# Claude Code Hooks

> Hooks 层在每次 Claude Code 执行特定操作后自动触发相应行为，是四层架构中最能产生质变的自动化机制。

## 核心要点

- Hooks 解决的核心问题：开发者需要手动管理大量与 AI 协作的元数据（上下文状态、窗口使用情况等）
- Hooks 的本质：把"每次做完某件事之后应该干什么"自动化
- Hooks 是 [[products/everything-claude-code]] 四层架构中的自动化层，最容易被忽视但最能产生质变

## 详细说明

Hooks 层通过自动化解决认知负担问题：开发者不用再分心管理和 AI 对话的元数据工作。

除了 memory-persistence、suggest-compact 这种“会话级自动化”，Hooks 也是工具执行管线里的策略注入点。以工具调用为中心看，PreToolUse Hook 发生在真正执行前，可用于阻止危险动作、改写输入或附加策略；PostToolUse Hook 则在执行后承担结果过滤、审计记录、自动 lint/format 等后处理职责。

## 关键 Hook 示例

### memory-persistence hook

**功能**：会话开始时自动加载上下文，会话结束时自动保存状态。

**效果**：下次打开项目时，Claude Code 知道你上次做到哪了，知道有哪些未解决的问题，不需要你重新介绍背景。

**解决的问题**：传统使用方式中，每次新对话都需要重复介绍项目背景和当前进度。

### suggest-compact hook

**功能**：当上下文窗口快满时，主动提醒你做精简。

**效果**：避免在某时间点突然发现 token 被耗尽，而不是在危机发生时才补救。

**解决的问题**：上下文窗口管理的被动性。

## 在四层架构中的位置

- **Rules**：规范层 — 代码标准是什么
- **Skills**：技能层 — 任务如何拆解
- **Hooks**：自动化层 — 完成后自动干什么（本文档）
- **Agents**：委托层 — 任务交给谁

## 与 [[concepts/layered-memory]] 的关联

memory-persistence hook 与 Hermes Agent 的分层持久化记忆体系有相似的目标——让 Agent 记住跨会话的上下文。两者都是解决"上下文丢失"问题的机制。

## 关联页面

- [[products/everything-claude-code]] — Hooks 所属的四层配置体系
- [[concepts/layered-memory]] — 相似的上下文持久化思路（Hermes Agent）
- [[patterns/claude-code-config-layers]] — 分层配置的整体思路
- [[concepts/tool-execution-pipeline]] — Hooks 在单次工具调用中的前后置位置
- [[concepts/harness-engineering]] — Hook 所处的更大 Harness 安全边界

## 参考来源

- 微信公众号：154K Star！Anthropic黑客松冠军的Claude Code配置大公开（2026-04-14）
- 用户输入文章《一次工具调用背后经历了什么？以 Claude Code 为例展开聊聊》（2026-04-17 收录）
