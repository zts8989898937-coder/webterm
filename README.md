# webterm

自托管网页终端与 AI CLI 会话前端：基于 `ttyd` + `tmux` + Node.js 同源反代，支持多标签、左右分屏、快捷键切屏（`Alt+←/→`）、剪贴板贴图上传（`⌘V`）以及 Codex / Antigravity 会话历史解析与配额状态面板。

## 核心组件

- `server.js`：Node.js 同源反代（HTTP Basic Auth 鉴权、`/paste` 贴图上传、`/tty` WebSocket 反代、`/close` 会话关闭）。
- `ttyd-session.sh` & `tmux.conf`：拉起与管理持久化 `tmux` 终端会话。
- `index.html`：前端终端界面，包含标签栏、左右分屏、快捷键与折叠对话视图。
- `history-parser.js` / `codex-history.js` / `codex-rollout.js` / `inline-predict.js`：历史记录解析、展开与补全辅助。
- `quota.js` / `quota-live-server.js` / `quota-sync.js` / `token-usage.js` / `agy-native-usage.js`：模型配额与 Token 用量统计模块。
- `*.test.js` / `*.test.cjs`：UI、滚动、分屏交换与历史解析回归测试。

## 部署前配置

服务依赖 Node.js、`ttyd`、`tmux`，会话脚本默认使用 Fish。先检查 `server.js` 中的目录和端口，以及 `ttyd-session.sh` 中的配置文件路径和默认 Shell。反代下游默认连接 `127.0.0.1:3901`。

启动时通过私有环境提供 `WEBTERM_PASS`，留空或使用脱敏占位符会拒绝启动。可用 `WEBTERM_USER` 设置登录名。网关默认监听 `127.0.0.1:3902`，局域网部署时通过 `WEBTERM_HOST` 指定本机局域网地址。部署范围为本机和局域网。

## 验证

```bash
node --test runtime-config.test.js history-parser.test.js codex-history.test.js codex-rollout.test.js native-menu.test.js
```

浏览器回归脚本依赖正在运行的服务、鉴权和会话环境，使用前需按本机环境调整。

## 2026-11-18 公开版更新

新增启动配置检查与单测。密码由私有环境变量提供，默认绑定回环地址。 [查看更新提交](https://github.com/zts8989898937-coder/webterm/commit/b33cce43da805c7e62505ea8d00ff497d5458259)

[公开范围](PUBLIC_SCOPE.md) · [架构说明](docs/ARCHITECTURE.md) · [后续路线](docs/ROADMAP.md)
