# Skill System（技能系统）

> 智能体将有效工作流自动抽象为可复用程序化流程的能力，既是人类编写技能的补充，也是自我进化记忆体系的核心组件。

## Hermes 的技能观

Hermes 认为：已完成的工作流可以被抽象为技能，即**可复用的程序化流程**（程序化知识），能够编码多步操作行为。

系统根据经验**自动生成**新技能，在执行过程中不断完善，并作为动态记忆层存储在 `~/.hermes/skills/` 目录下。

## 技能管理

- 智能体通过 `skill_manage` 工具按需**创建、优化和调用**技能
- 支持**跨会话持续学习**
- 可通过 **Skills Hub** 安装更多技能（集成多个技能注册中心，遵循 agentskills.io 开放标准）

## 与 OpenClaw 技能的对比

| 维度 | Hermes 技能 | OpenClaw 技能 |
|------|-------------|---------------|
| 来源 | 自动生成 + 人类优化 | 主要由人类编写 |
| 定位 | 自我改进学习体系的一部分 | 模块化插件/指令包 |
| 动态性 | 执行过程中不断完善 | 相对静态 |
| 存储 | `~/.hermes/skills/` | 按工作区/个人/共享/插件范围加载 |

## 本质意义

技能可视为内存栈的第四层（程序性记忆层）。这一设计让智能体从"记住事实"转向"记住方法"——本质是自我进化范式在技能层面的落地。

## 关联页面

- [[concepts/agent-memory]]
- [[concepts/hermes-agent]]
- [[concepts/self-evolution]]
- [[concepts/layered-memory]]
- [[concepts/openclaw]]

## 参考文档

- Hermes 技能系统文档：https://hermes-agent.nousresearch.com/docs/user-guide/features/skills/
- Hermes Agent vs OpenClaw 解析：微信公众号文章（2026-04-14）
- 微信公众号：浅谈 Agent Memory（2026-04-12）— 将 Skills 明确放入“程序性记忆”语境
