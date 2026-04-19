# Nginx + PM2 + Next.js 单机部署模式

> 用 Nginx 做公网入口、PM2 托管 Next.js 进程、PostgreSQL 留在本机，是早期 Web 项目在单台云服务器上快速上线的低复杂度部署模式。

## 问题场景

这个模式适合首发阶段的单体 Web 项目，尤其是：

- 项目需要尽快上线验证主流程。
- 团队暂时不想引入容器编排、负载均衡和托管数据库。
- 应用是 Next.js 这类 Node.js 服务端渲染或全栈项目。
- 数据库访问量不大，可以先与应用同机部署。

它不适合已经有高可用、弹性扩容、灰度发布、多服务治理要求的系统。

## 解决方案

核心链路是：

```text
用户浏览器
  -> Nginx 监听 80/443
  -> 反向代理到 127.0.0.1:3000
  -> PM2 托管 Next.js 的 pnpm start
  -> 本机 PostgreSQL
```

各组件职责要分清：

- **Nginx**：只作为公网入口，负责标准端口、反向代理、后续 HTTPS、证书和路径分发。
- **PM2**：只负责 Node.js 进程守护、日志、异常重启和配合 systemd 开机恢复。
- **Next.js**：只监听本机内部端口，不直接暴露公网。
- **PostgreSQL**：首发阶段可同机运行，但不要开放 `5432` 到公网。

最小验证顺序应该是：

1. `curl -I http://127.0.0.1:3000`
2. `curl -I http://服务器IP`
3. `pm2 status`
4. `systemctl status pm2-<user>`
5. `sudo nginx -t`
6. `sudo -u postgres psql -d <db> -c '\dt'`

## 权衡取舍

优点：

- 部署链路短，排障边界清楚。
- 成本低，适合首发验证。
- 不需要一开始就引入 Kubernetes、Docker Swarm 或复杂 CI/CD。

代价：

- 单点故障明显。
- 数据库和应用同机，资源竞争需要关注。
- 规模增长后需要迁移到托管数据库或多实例架构。

这个模式的关键不是“永远单机”，而是用单机降低首发验证成本。业务验证成功后，再按真实瓶颈升级架构。

## 关联页面

- [[patterns/pm2-systemd-handoff]]
- [[patterns/deployment-entry-layer-validation]]
- [[patterns/nextjs-subpath-deployment]]
- [[concepts/engineering-sense]]
- [[patterns/agent-workflow-calibration]]

## 参考来源

- 本机项目部署文档：`/Users/paulchess/Desktop/Home/entrepreneurship/enterprise-ai-survey/docs/deployment/企业AI转型评估H5腾讯云部署全流程实战记录.md`（2026-04-19）
