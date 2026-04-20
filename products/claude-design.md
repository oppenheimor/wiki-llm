# Claude Design

> Anthropic Labs 推出的对话式视觉设计产品，让团队通过与 Claude 协作生成设计稿、交互原型、演示文稿和可交付给工程的 handoff 资产。

## 核心能力

- **对话生成视觉产物**：可直接通过聊天生成 designs、interactive prototypes、slides、one-pagers 等视觉内容。
- **自动继承团队设计系统**：在完成组织级设计系统接入后，项目会自动使用品牌色、字体和组件模式，减少每次重复设定。
- **多源上下文输入**：支持从文本提示开始，也可补充截图、图片、文档、代码仓库和现有设计文件，让输出更接近真实产品。
- **从设计到工程 handoff**：设计完成后可一键导出为 HTML、PDF、PPTX，或直接 handoff 给 Claude Code / 本地 coding agent。
- **组织内协作与分享**：支持组织范围内的 view-only、comment、edit 分享，以及多人共同和 Claude 迭代同一设计。

## 技术亮点

### 它把“设计生成”做成了 Claude 内部原生工作流
Claude Design 不是单次图像生成入口，而是一个左侧聊天、右侧画布的持续协作环境。用户可以混合使用聊天、画布内评论、直接文本编辑和 Claude 生成的自定义滑杆，对同一设计反复迭代。

### 设计系统接入被前置成产品能力
Anthropic 新闻页强调，Claude Design 会在 onboarding 阶段读取团队代码库和设计文件，构建可复用的 design system；帮助中心则说明后续新项目默认继承该系统。这让它更像“把品牌与组件约束嵌进生成流程”，而不是纯自由生成工具。

### 交付链路直接连到 Canva 与 Claude Code
它不仅支持 PDF、PPTX、standalone HTML 等传统导出，还支持发送到 Canva，以及把设计打包为 handoff bundle 交给 Claude Code。这个组合说明 Claude Design 的定位是连接设计探索、团队协作和实现交付的前置层。

### 当前仍处于研究预览阶段
截至 2026-04-17 发布新闻与 2026-04-20 查阅帮助中心时，Claude Design 处于 research preview / experimental preview。帮助中心列出的已知限制包括评论偶发丢失、compact view 保存报错、大代码库导入卡顿，以及 `chat upstream error` 时建议在同项目内新开 chat tab。

## 使用场景

- 设计师快速扩展多版探索方向，把静态 mockup 转成可分享、可测试的交互原型
- 产品经理先画 feature flow 或 wireframe，再交给设计师细化或 handoff 给 Claude Code 实现
- 创始人、销售或市场团队快速做 on-brand pitch deck、landing page、campaign visual
- 团队围绕已有代码库、设计文件和品牌规范，在同一画布里协作迭代并导出交付物

## 关联页面

- [[concepts/claude-code-skills]]
- [[patterns/design-skill-layering]]
- [[products/ui-ux-pro-max]]
- [[products/claude-agent-sdk]]

## 参考来源

- Anthropic 官方新闻《Introducing Claude Design by Anthropic Labs》（https://www.anthropic.com/news/claude-design-anthropic-labs，2026-04-20 通过 CDP 查阅）
- Claude 帮助中心《Get started with Claude Design》（https://support.claude.com/en/articles/14604416-get-started-with-claude-design，2026-04-20 通过 CDP 查阅）
