# Next.js 子路径部署模式

> 当 Next.js 应用要部署到 `/<app-name>` 这类子路径时，应优先让应用通过 `basePath` 原生理解部署前缀，再由 Nginx 代理对应路径。

## 问题场景

这个模式适用于：

- 应用正式入口不是域名根路径，而是类似 `/enterprise-ai-survey` 的子路径。
- 同一个域名或 IP 下面需要区分不同入口。
- 需要保证页面跳转、静态资源、API 请求和缓存失效路径都与子路径一致。

常见误区是：只在 Nginx 层把 `/app` rewrite 到 `/`，以为这样应用就完成了子路径部署。

## 解决方案

正确顺序是：

1. 在 Next.js 配置中声明 `basePath`。
2. 重新构建应用，因为 `basePath` 是构建期配置。
3. 检查应用中不会自动加前缀的路径，例如裸 `fetch("/api/...")`。
4. 用 Nginx 代理子路径到应用本机端口。
5. 分别验证首页、子页面、API、静态资源和根路径行为。

示例：

```js
// next.config.mjs
const nextConfig = {
  basePath: process.env.NEXT_PUBLIC_BASE_PATH || "/enterprise-ai-survey",
};

export default nextConfig;
```

需要特别区分：

- `next/link` 会自动应用 `basePath`，不要手工再拼一次。
- 客户端裸 `fetch("/api/...")` 不会自动应用 `basePath`，需要显式处理。
- `revalidatePath("/dashboard")` 按路由文件路径工作，不应该拼 `basePath`。
- CSS 中的根路径资源，例如 `url("/fonts/...")`，在子路径部署时容易漂移，优先改为 `next/font/local` 或其他由构建系统管理的资源路径。

Nginx 层只负责把请求转给应用，不应承担“让应用误以为自己运行在子路径”的所有语义。

## 权衡取舍

优点：

- 路由、静态资源、API 和页面跳转语义一致。
- 后续维护比 Nginx 大量 rewrite 更清楚。
- 本地测试与线上行为更容易对齐。

代价：

- 修改 `basePath` 后必须重新构建。
- 需要审计项目里的根路径写法。
- 如果应用已经大量硬编码绝对路径，迁移会有一定成本。

判断标准：

- 只想临时演示，可以用 Nginx 伪子路径。
- 要稳定上线，应使用 Next.js `basePath`。

## 关联页面

- [[patterns/nginx-pm2-nextjs-single-host-deployment]]
- [[patterns/deployment-entry-layer-validation]]
- [[patterns/prompt-as-system-design]]
- [[concepts/engineering-sense]]

## 参考来源

- 本机项目部署文档：`/Users/paulchess/Desktop/Home/entrepreneurship/enterprise-ai-survey/docs/deployment/企业AI转型评估H5腾讯云部署全流程实战记录.md`（2026-04-19）
- 本机项目设计文档：`/Users/paulchess/Desktop/Home/entrepreneurship/enterprise-ai-survey/docs/plans/2026-04-19-enterprise-ai-survey-subpath-deployment-design.md`（2026-04-19）
