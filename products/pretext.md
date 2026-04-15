# Pretext

> 纯 JavaScript/TypeScript 多行文本测量与布局库。不触碰 DOM、不触发 reflow，用浏览器字体引擎作为地面真值（ground truth）做精确测量。支持 DOM、Canvas、SVG 渲染，服务端渲染也在路上。

npm 包名：`@chenglou/pretext`，仓库：https://github.com/chenglou/pretext，作者 Cheng Lou。

## 解决的核心问题

浏览器里测文本高度通常要靠 `getBoundingClientRect`、`offsetHeight` 这类 DOM 查询，每次都会触发 layout reflow —— 浏览器里最贵的操作之一。Pretext 完全绕开 DOM 测量：自己实现文本测量逻辑，底层只用 canvas `measureText` 作为字形宽度真值。

为什么这很重要：reflow 在高频交互（拖拽、resize、流式渲染长文本）里会卡顿，而用 JS 纯算术算高度没有这个代价。

## 两种使用范式

### ① 仅测量段落高度（不碰 DOM）

典型 API：`prepare()` + `layout()`

```js
import { prepare, layout } from '@chenglou/pretext'
const prepared = prepare('AGI 春天到了. بدأت الرحلة 🚀', '16px Inter')
const { height, lineCount } = layout(prepared, textWidth, 20)
```

- `prepare()` 做一次性重活：规范化空白、分段、应用 glue 规则、用 canvas 测各段宽度，返回不透明句柄
- `layout()` 是热路径：对缓存宽度做纯算术，resize 时只需重跑它
- 禁忌：同一段文本和配置不要重复 `prepare()`，那会抵消预计算

**解锁的场景**：
- 不靠猜测和缓存的虚拟化/遮挡（virtualization/occlusion）
- 用户态 fancy 布局：masonry、JS 驱动的类 flexbox、绕过 CSS hack 直接调参
- 开发期验证（尤其配合 AI）——按钮 label 不会溢出换行，无需开浏览器
- 新文本加载时防抖动（layout shift），重新锚定滚动位置

### ② 手动逐行布局

典型 API：`prepareWithSegments()` 配合 `layoutWithLines` / `walkLineRanges` / `layoutNextLineRange` / `materializeLineRange` 等

核心能力：
- **固定宽度多行布局**：`layoutWithLines` 一次给你所有行
- **只要统计不要字符串**：`measureLineStats` / `walkLineRanges` 返回行数与宽度但不构造文本字符串
- **变宽度流式布局**：`layoutNextLineRange` 按光标一行一行要，每行可传不同 maxWidth —— 用于图文绕排（浮动图片旁的行更窄）、列宽动态变化
- **收缩包裹宽度**：`walkLineRanges` 可配合 `measureNaturalWidth` 找到「最紧但仍能容纳文本的容器宽度」—— 这个「shrink wrap」一直缺失于 Web

可渲染到 canvas、SVG、WebGL，未来计划支持服务端渲染。

### 富文本内联流助手

`@chenglou/pretext/rich-inline` 子模块，专为内联级富文本排版（代码片段、@mentions、chip 标签等）：
- 输入是原始 inline items 数组，每项自带 `font`、`break: 'never'`（原子不拆分）、`extraWidth`（caller 自己负责的 padding/border 宽度）
- 由编译器统一处理跨 item 的空白折叠
- 有意保持狭窄：仅支持 `white-space: normal` 内联流，不是通用 CSS inline formatting engine，也不是嵌套 markup 树

## 设计要点

- **Segment/grapheme 光标而非字符串偏移**：`LayoutCursor` 不是 string offset，而是段索引 + 字素索引，天然处理多字节、emoji、组合字符
- **`prepare` 只做水平向工作**：`lineHeight` 留到 layout 阶段作为输入 —— 同一份 prepared 可以在不同行高下复用
- **软连字符破行**：若软连字符赢得断点，materialized 行文本会包含可见的尾部 `-`
- **双向文本**：richer handle 包含 `segLevels` 用于自定义 bidi 感知渲染；line-breaking API 不读它
- **段宽 ≠ 字形坐标**：段宽是浏览器 canvas 宽度用于断行，不是用来做自定义阿拉伯语或混向排版的精确字形位置数据

## 支持与限制

**支持**：
- `white-space: normal` 和 `pre-wrap`
- `word-break: normal` 和 `keep-all`（CJK/Hangul 行为符合预期）
- `overflow-wrap: break-word`（极窄宽度下按字素边界破词）
- `line-break: auto`
- 默认浏览器式 `tab-size: 8`

**不支持/陷阱**：
- `system-ui` 在 macOS 上对 `layout()` 的精度不安全，必须用具名字体
- 不是完整字体渲染引擎
- `font` 参数必须与 CSS `font` shorthand 同步（size/weight/style/family）
- `lineHeight` 参数必须与 CSS `line-height` 同步

## 与 AI 工程化的关联

README 明确提到两处 AI 相关意图：
1. 「用浏览器字体引擎作为 ground truth」是 "very AI-friendly iteration method" —— 即实测对照样本可以喂给模型做迭代验证
2. 「development time 验证，尤其现在有 AI 了」—— 让 AI 生成 UI 时能无头校验 label 不会溢出换行

## 安装与 Demo

```bash
npm install @chenglou/pretext
```

本地 demo：`bun install && bun start`，浏览器打开 `/demos/index`（Windows 用 `bun run start:windows`）。线上 demo：chenglou.me/pretext 和 somnai-dreams.github.io/pretext-demos。

## 历史渊源

Sebastian Markbage 十年前的 [text-layout](https://github.com/chenglou/text-layout) 是起点。他当年的架构 —— canvas `measureText` 做塑形、从 pdf.js 移植 bidi、流式行断开 —— 是 Pretext 继承并推进的蓝本。

## 关联页面

（暂无）

## 参考来源

- GitHub README：https://github.com/chenglou/pretext（2026-04-15 收录）
- 包名：`@chenglou/pretext`
- 前身：https://github.com/chenglou/text-layout
