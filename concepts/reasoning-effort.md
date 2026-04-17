# Reasoning Effort（推理强度）

> 让模型在响应速度、token 消耗与推理深度之间调节权衡的配置层；在 Anthropic/Claude 语境里，`effort` 用来取代显式的 thinking budget 调参。

## 核心要点

- **`effort` 是比 thinking budget 更高层的旋钮**：用户不再直接控制“想多少 token”，而是控制模型总体上“想得更快还是更深”。
- **Adaptive thinking 把预算细节藏到系统内部**：以 Opus 4.7 为例，模型会根据任务难度自适应分配思考量，而不是要求用户手动设 budget。
- **不同 effort level 对应速度/成本/能力的不同平衡点**：较低 effort 更快、更省 token；较高 effort 更慢，但通常能换来更强的推理和复杂任务表现。
- **配置语义可能区分“会话内临时值”和“跨会话持久值”**：在这段材料里，`max` 只作用于当前 session，而其他 effort level 会持久到后续 session。

## 详细说明

### 从 thinking budgets 到 effort

早期很多推理模型或推理接口会暴露 thinking budget 一类的参数，让用户直接决定模型最多花多少“思考资源”。这虽然精细，但也把底层资源分配复杂度甩给了用户。

`effort` 的设计更像一个产品化后的抽象层：用户只需要表达“我要更快”还是“我要更强”，具体如何在内部平衡 token、延迟与思考深度，则交给模型的 adaptive thinking 机制处理。

### 配置层的几个典型档位

这段材料明确提到 `lower`、`higher`、`xhigh` 和 `max` 一类 effort level。核心区别不是功能开关，而是推理资源分配强度的差异。

一个重要细节是 `max` 与其他档位的生命周期不同：`max` 只对当前 session 生效，而其他 effort level 会成为 sticky 配置，继续影响后续 session。这个语义差异很适合被记录在知识库里，因为它会直接影响实际使用体验。

### `/effort` 作为用户控制面

这段材料还透露了一个典型交互界面：通过 `/effort` 命令切换当前 effort level。也就是说，effort 不是纯 API 参数，而是进入了 Claude 类产品的交互式工作流，成为用户主动调节思考强度的前台控制面。

## 上下文

这个概念适合放在 Agent / Coding Assistant 的运行时配置语境中理解：它描述的不是某个单一工具，而是“模型在当前会话里愿意投入多少推理资源”的用户控制层。

## 关联页面

- [[concepts/agent-loop]]
- [[concepts/tokenization]]
- [[concepts/claude-code-rules]]
- [[products/claude-agent-sdk]]

## 参考来源

- 用户输入短文《Configure your effort level》（收录于 2026-04-17）
