# Claude Code Rules

> Rules 层定义项目的代码规范，将其编码为 Claude Code 的默认行为，无需每次对话重新说明。

## 核心要点

- Rules 解决的核心问题：开发者每次使用 Claude Code 时都需要重复解释项目规范、代码风格偏好、测试覆盖率要求等上下文信息
- Rules 的本质：将"你每次都要说的话"变成 Claude Code 的默认行为
- Rules 是 ECC 四层架构（Rules/Skills/Hooks/Agents）中的第一层，负责代码规范层

## 详细说明

在传统使用方式中，Claude Code 更像一个高级对话框：遇到问题 → 描述上下文 → 等结果 → 再描述。这种方式的隐性成本是每次都要重新解释上下文。

Rules 层通过预置配置文件，将以下信息编码为持久化的默认行为：
- 项目代码规范（命名约定、文件组织）
- 代码风格偏好（格式化、注释规范）
- 测试覆盖率要求
- 包管理器偏好（pnpm / bun / npm）

## 在四层架构中的位置

[[products/everything-claude-code]] 的四层架构各司其职：
- **Rules**：规范层 — 定义代码标准
- **Skills**：技能层 — 任务如何拆解
- **Hooks**：自动化层 — 完成后自动干什么
- **Agents**：委托层 — 任务交给谁

## 关联页面

- [[products/everything-claude-code]] — Rules 所属的四层配置体系
- [[patterns/claude-code-config-layers]] — Rules/Skills/Hooks/Agents 的分层思路

## 参考来源

- 微信公众号：154K Star！Anthropic黑客松冠军的Claude Code配置大公开（2026-04-14）
