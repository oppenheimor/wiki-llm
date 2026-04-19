# 部署入口分层验收模式

> 部署验收应按本机端口、Nginx 公网入口、域名/CDN、业务流程、数据层逐层推进，避免把入口问题误判为应用问题。

## 问题场景

Web 项目部署失败时，经常会混淆几类不同问题：

- 应用进程没启动。
- Nginx 还在使用默认站点。
- 数据库连接串错误。
- 域名仍指向 Cloudflare 或旧 CDN。
- API 路径已经打到正确应用，但请求方法不匹配。
- 页面能打开，但数据没有落库。

如果一开始就用域名做唯一验收口径，很容易把 DNS、CDN、Nginx、应用和数据库问题搅在一起。

## 解决方案

按层验收：

1. **应用本机层**
   - `curl -I http://127.0.0.1:3000`
   - 验证 Next.js 自身是否运行。

2. **Nginx 公网层**
   - `curl -I http://服务器IP`
   - 验证公网请求是否被 Nginx 正确代理。

3. **子路径层**
   - `curl -I http://服务器IP/<app-name>`
   - `curl -I http://服务器IP/<app-name>/dashboard`
   - 验证入口前缀是否正确。

4. **API 层**
   - 对 API 路径做 `HEAD` 或最小请求。
   - 注意 `405 Method Not Allowed` 不一定是坏事，它可能说明已经命中正确 Route Handler，只是方法不匹配。

5. **域名层**
   - `dig +short example.com`
   - 验证域名是否指向当前服务器 IP，而不是旧 CDN 或 Cloudflare。

6. **数据层**
   - `psql -c '\dt'`
   - 或提交真实表单后查询业务表。

## 权衡取舍

优点：

- 快速定位问题属于哪一层。
- 避免把 DNS 或 Nginx 问题误判成应用代码问题。
- 适合作为首发部署和上线复盘的标准检查清单。

代价：

- 验收步骤比“打开浏览器看一眼”更繁琐。
- 需要明确每一层的预期响应，而不是机械追求所有请求都返回 200。

关键判断：

- IP 不通，优先看应用、PM2、Nginx。
- IP 通但域名不通，优先看 DNS、Cloudflare、备案和证书。
- 页面通但业务不通，继续看 API、环境变量和数据库。

## 关联页面

- [[patterns/nginx-pm2-nextjs-single-host-deployment]]
- [[patterns/nextjs-subpath-deployment]]
- [[patterns/pm2-systemd-handoff]]
- [[concepts/engineering-sense]]
- [[patterns/agent-workflow-calibration]]

## 参考来源

- 本机项目部署文档：`/Users/paulchess/Desktop/Home/entrepreneurship/enterprise-ai-survey/docs/deployment/企业AI转型评估H5腾讯云部署全流程实战记录.md`（2026-04-19）
