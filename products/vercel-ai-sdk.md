# Vercel AI SDK

> 面向 AI 应用构建的全栈 SDK，核心价值不只是“调模型”，而是提供从后端流式协议到前端消息消费的统一抽象，尤其适合快速搭建带结构化流式 UI 的 Agent 产品。

## 核心能力
- **统一模型与 UI 层抽象**：既有模型接入层，也有把后端流式消息传给前端的 UI 协议与客户端 Hook。
- **内置 Data Stream Protocol**：把文本、工具输入、工具输出等交互编码成前端可消费的事件流。
- **前端消费体验完整**：React、Vue 等前端可以直接用现成客户端解析消息流，而不必手写 SSE 协议解析器。
- **可与其他 Agent 框架拼接**：并不要求必须用它来写完整 Agent；也可以只复用 UI 协议层，把 LangChain 之类框架产出的流转成它的消息格式。
- **工具可视化友好**：消息被拆成 `parts` 后，前端能按 part 类型渲染文本块、工具卡片、结果区块等不同组件。

## 技术亮点
### 它把“协议”做成了产品能力
很多团队以为自己缺的是一个聊天组件，实际上缺的是一套前后端都认可的流式事件协议。Vercel AI SDK 把这层抽象为 Data Stream Protocol，并配套传输与消费工具，省掉了大量手写协议胶水代码。

### 可只用 UI，不绑死 Agent 框架
它既可以自己承担模型调用，也可以只作为 UI 协议层使用。和 LangChain 之类 Agent 框架搭配时，后端继续用擅长的 Agent 编排框架，前端则复用 AI SDK 的流式消息消费能力，这是很典型的“局部采用”路径。

### 前端不再操作原始 SSE
传统做法里，前端往往直接处理原始 SSE 文本，再手工拆协议。使用 AI SDK 后，前端更接近“消费消息对象”，而不是“处理流分隔符与状态机”。

## 使用场景
- 需要把纯文本 Agent 升级为带工具卡片、状态组件的可视化 UI
- 后端已有 LangChain / 自研 Agent，希望复用成熟的流式 UI 协议
- 需要 React / Vue 端快速接入统一的聊天与工具渲染消息流
- 希望减少前后端围绕 SSE 文本格式反复对齐的沟通成本

## 关联页面
- [[concepts/agui-protocol]]
- [[patterns/tool-aware-streaming-ui]]
- [[concepts/agent-loop]]
- [[concepts/harness-engineering]]
- [[products/langgraph]]

## 参考来源
- 用户输入文章《AGUI 协议：Vercel AI SDK + LangChain 实现流式组件渲染 已付费》（2026-04-16 收录）
- Vercel AI SDK 文档：Data Stream Protocol（用户提供链接与教程摘要）
