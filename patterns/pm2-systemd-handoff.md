# PM2 与 systemd 接管模式

> PM2 的 `startup` 和 `save` 只是开机恢复链路的一部分，真正可靠的上线必须确认 systemd 已经成功接管 PM2 daemon。

## 问题场景

Node.js 应用用 PM2 托管后，经常会执行：

```bash
pm2 startup
pm2 save
```

很多人看到 `systemctl is-enabled pm2-xxx` 返回 `enabled`，就以为开机自启已经完成。

但实际可能出现：

- `pm2-xxx.service` 是 `enabled`
- `systemctl status pm2-xxx` 却是 `failed`
- 应用当前在线，但服务器重启后无法恢复

这类问题在“先手工启动 PM2 daemon，再让 systemd 接管”时尤其常见。

## 解决方案

正确检查顺序：

```bash
pm2 status
systemctl is-enabled pm2-<user>
systemctl status pm2-<user> --no-pager
```

若 systemd 接管失败，日志里可能出现：

```text
New main PID ... does not belong to service
Can't open PID file ... pm2.pid
```

可采用以下修复流程：

```bash
sudo -u <user> pm2 save
sudo -u <user> pm2 kill
sudo systemctl reset-failed pm2-<user>
sudo systemctl start pm2-<user>
systemctl status pm2-<user> --no-pager
sudo -u <user> pm2 status
```

核心思想是：先保存进程列表，再杀掉手工启动的 PM2 daemon，让 systemd 以正确身份重新拉起 PM2。

## 权衡取舍

优点：

- 能把“当前进程在线”升级为“重启后可恢复”。
- 排除了 enabled 但 failed 的假自启状态。

代价：

- 切换接管时会短暂重启应用。
- 需要理解 PM2 daemon、PM2 应用进程和 systemd service 不是同一层东西。

上线时至少要确认：

- `pm2 status` 中应用是 `online`
- `systemctl status pm2-<user>` 是 `active`
- 经过一次“PM2 kill 后由 systemd 拉起”的恢复验证

## 关联页面

- [[patterns/nginx-pm2-nextjs-single-host-deployment]]
- [[patterns/deployment-entry-layer-validation]]
- [[patterns/agent-always-on-host]]

## 参考来源

- 本机项目部署文档：`/Users/paulchess/Desktop/Home/entrepreneurship/enterprise-ai-survey/docs/deployment/企业AI转型评估H5腾讯云部署全流程实战记录.md`（2026-04-19）
