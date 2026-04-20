# UI/UX Pro Max

> 面向 UI/UX 任务的设计智能 skill，把风格、配色、字体、图表、页面结构和技术栈建议组织成可检索、可组合的设计知识库。

## 核心能力

- **多维设计检索**：覆盖 style、color、typography、landing、chart、ux、stack 等多个领域，适合把模糊的设计诉求拆成具体决策。
- **从风格到实现一条龙**：既能给视觉方向，也能给 React、Next.js、Tailwind、shadcn/ui 等栈的实现建议。
- **默认服务于生成式 UI 工作流**：特别适合“没有设计稿但要先做出一个像样界面”的场景。
- **支持按产品类型反查设计语言**：可从 SaaS、dashboard、landing page、portfolio 等产品类型出发，再回到对应的颜色、字体和版式建议。

## 技术亮点

### 它不是单条 prompt，而是结构化设计知识库
Skill 文件把 UI/UX 能力拆成多个可搜索域，再通过 `search.py` 做检索式调用。这种设计比“直接让模型自由发挥”更稳定，因为它先约束检索空间，再组织输出。

### 设计建议和实现栈绑在一起
它不只讲“好不好看”，还内置了 `html-tailwind`、`react`、`nextjs`、`shadcn` 等栈的具体指南。这说明它的定位更像“面向交付的设计 intelligence”，而不是灵感画廊。

## 使用场景

- 没有设计稿时，为产品快速生成完整且风格统一的首版 UI
- 需要给 landing page、dashboard、admin panel 等页面先定视觉方向
- 希望把设计决策从“拍脑袋”变成“先检索、再组合、后实现”
- 在 AI 驱动前端开发里，把设计知识作为可复用 skill 资产加载

相较于 Anthropic 官方的 [[products/claude-design]]，UI/UX Pro Max 更偏“本地可检索设计知识库 + 生成建议”，而不是带组织协作、设计系统继承和工程 handoff 的完整产品界面。

## 关联页面

- [[concepts/claude-code-skills]]
- [[products/claude-design]]
- [[concepts/skill-system]]
- [[patterns/anti-ai-slop-frontend-prompting]]
- [[patterns/design-skill-layering]]
- [[patterns/same-content-style-wall-screening]]

## 参考来源

- 本机 skill：`/Users/paulchess/.codex/skills/ui-ux-pro-max/SKILL.md`（2026-04-17 查阅）
- 微信公众号《程序员必备的 Design Skills，不要让 UI 成为产品短板》（壹零笔记，2026-03-17，2026-04-17 通过 CDP 抓取）
