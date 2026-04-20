# Design Skill Layering

> 不把 UI 设计能力当成一个“大一统工具”来选，而是按项目阶段拆成生成、整理、还原、系统化四层，再为每层匹配不同 skill 组合。

## 问题场景

很多程序员在做 UI 时会掉进两个常见误区：
- 没有设计稿时，直接让 AI 或组件库随手拼一个页面，结果结构散、气质弱、像内部 Demo
- 已有页面或设计稿时，仍然用同一把锤子解决所有问题，导致该做规范整理的阶段去重画界面，该做精细还原的阶段却还在讨论风格

真正缺的往往不是“某一个更强的 UI 工具”，而是把设计问题先分层。

## 解决方案

先按阶段识别当前问题属于哪一层：

- **生成层**：没有设计图，目标是先做出结构完整、风格统一的首版界面
- **整理层**：已有存量 UI，目标是统一 spacing、字体、颜色和组件逻辑
- **还原层**：已有设计稿，目标是把间距、状态、动效和细节精确落地
- **系统化层**：项目进入团队或长期维护阶段，目标是把设计能力嵌进 agent、审计和开发流程

然后再做 skill 组合，而不是执着于某个名字本身。文章里提到的 `UI UX Pro Max`、`UI Skills`、`Impeccable`、`Vercel Web Design Guidelines` 等，本质上分别服务于不同阶段的能力缺口。到 2026-04-20 查阅的 Anthropic 官方 [[products/claude-design]]，则把这种“按阶段反复生成与收敛”的设计工作流产品化成了 Claude 内部原生界面：先生成首版，再通过评论、对话和 handoff 持续推进。

如果当前卡点不是“缺少工具”，而是“生成结果总带平均审美味道”，那问题就不只属于生成层，还需要叠加 [[patterns/anti-ai-slop-frontend-prompting]] 这类专门约束默认审美收敛的提示模式。

## 权衡取舍

这套模式的好处是：讨论会更聚焦，团队不再争“哪个 skill 最强”，而是先问“当前卡在哪一层”。它也能减少误用，例如把本该做规范收敛的问题误判成“再生成一个更炫的页面”。

代价同样明确：
- 你需要先判断问题阶段，不能把所有 UI 请求都当成单步生成任务
- skill 名称会变，但分层逻辑应该保持稳定，因此沉淀时要优先记录“能力类别”而不是品牌名

## 关联页面

- [[concepts/claude-code-skills]]
- [[concepts/skill-system]]
- [[products/claude-design]]
- [[products/ui-ux-pro-max]]
- [[patterns/anti-ai-slop-frontend-prompting]]
- [[products/superpowers]]
- [[patterns/same-content-style-wall-screening]]

## 参考来源

- 微信公众号《程序员必备的 Design Skills，不要让 UI 成为产品短板》（壹零笔记，2026-03-17，2026-04-17 通过 CDP 抓取）
- 本机 skill：`/Users/paulchess/.codex/skills/ui-ux-pro-max/SKILL.md`（2026-04-17 查阅）
- 本机 skill：`/Users/paulchess/.codex/skills/web-design-guidelines/SKILL.md`（2026-04-17 查阅）
- Anthropic 官方新闻《Introducing Claude Design by Anthropic Labs》（2026-04-20 通过 CDP 查阅）
- 用户粘贴文章《Claude Design 提示词指南：怎么 Vibe 出好看的 UI》（2026-04-20 收录）
