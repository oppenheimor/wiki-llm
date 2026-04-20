# Anti-AI-Slop Frontend Prompting

> 在生成式前端任务里，主动从字体、颜色、动效和背景四个维度约束模型的默认审美收敛，打断“平均分布”式安全输出。

## 问题场景

不带设计方向地让模型生成页面时，产物很容易落回一眼能认出的“AI 做的”样子：通用字体、保守配色、熟悉卡片布局、到处点缀但缺乏重点的微交互。Anthropic 官方前端审美指南直接把这类现象命名为 “AI slop” aesthetic，本质上是模型沿着训练分布里的安全均值滑行。

## 解决方案

不要只说“做得高级一点”，而是显式打断模型的默认路径：

- **字体**：避免 Inter、Roboto、Arial 这类过度安全的默认选项，明确指定字体气质与搭配原则，例如 display + monospace、serif + geometric sans、极端字重对比。
- **颜色**：先承诺一个主色方向，再用 CSS 变量统一系统，不要让页面每一块都平均分配色彩存在感。
- **动效**：把精力集中在高影响时刻，例如页面加载时的 staggered reveal，而不是给每个组件都塞一点零散动画。
- **背景**：用渐变、几何纹理或氛围层次建立视觉场，而不是默认纯色或老套紫色渐变白底。

在流程上，再叠加两个约束：

- 先要设计上下文，再要生成结果；没有上下文时优先索要代码库、截图、Figma、品牌说明或现有组件
- 先要多个方向，再要微调收敛；先出 3 个以上变体探索，再通过 Tweaks 一类机制在 80 分稿件上做局部迭代

## 权衡取舍

这套模式的收益是：UI 更容易摆脱模板感，团队讨论也从“好不好看”转向“这次到底在探索什么维度”。它尤其适合 vibe coding 阶段，因为它把“审美方向”从隐含偏好变成显式约束。

代价也很明确：

- 你需要先给产品类型、用户、品牌调性和探索方向，而不是一句话把判断全甩给模型
- 为了避免收敛回均值，往往要接受更高的前期提问密度和更多变体探索成本
- 这不是保证产出一定更好看，只是把失败模式从“默认平庸”换成“方向明确但仍需筛选”

## 关联页面

- [[products/claude-design]]
- [[products/ui-ux-pro-max]]
- [[patterns/design-skill-layering]]
- [[patterns/same-content-style-wall-screening]]
- [[concepts/vibercoding]]

## 参考来源

- Anthropic Cookbook《Prompting for frontend aesthetics》：https://platform.claude.com/cookbook/coding-prompting-for-frontend-aesthetics
- 用户粘贴文章《Claude Design 提示词指南：怎么 Vibe 出好看的 UI》（2026-04-20 收录）
