# webterm

自托管网页终端与 AI CLI 会话前端：基于 `ttyd` + `tmux` + Node.js 同源反代，支持多标签、左右分屏、快捷键切屏（`Alt+←/→`）、剪贴板贴图上传（`⌘V`）以及 Codex / Antigravity 会话历史解析与配额状态面板。

## 核心组件

- `server.js`：Node.js 同源反代（HTTP Basic Auth 鉴权、`/paste` 贴图上传、`/tty` WebSocket 反代、`/close` 会话关闭）。
- `ttyd-session.sh` & `tmux.conf`：拉起与管理持久化 `tmux` 终端会话。
- `index.html`：前端终端界面，包含标签栏、左右分屏、快捷键与折叠对话视图。
- `history-parser.js` / `codex-history.js` / `codex-rollout.js` / `inline-predict.js`：历史记录解析、展开与补全辅助。
- `quota.js` / `quota-live-server.js` / `quota-sync.js` / `token-usage.js` / `agy-native-usage.js`：模型配额与 Token 用量统计模块。
- `*.test.js` / `*.test.cjs`：UI、滚动、分屏交换与历史解析回归测试。

## 安全提示

本仓库为**脱敏公开版**，启动前必须通过私有环境设置 `WEBTERM_PASS`；缺失、空白或仍为脱敏占位符时拒绝启动。默认只监听 `127.0.0.1`，局域网部署时显式设置 `WEBTERM_HOST` 为本机局域网地址，可通过 `WEBTERM_USER` 设置登录名。终端仅供本机或局域网访问，不配置公网入口。请勿将真实凭据提交到版本库。

## 公开版本说明

部署参数使用示例值。公开范围见 [PUBLIC_SCOPE.md](PUBLIC_SCOPE.md)，通用框架和路线见 [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) 与 [docs/ROADMAP.md](docs/ROADMAP.md)。

## 验证

`node --test runtime-config.test.js history-parser.test.js codex-history.test.js codex-rollout.test.js native-menu.test.js` 可执行独立单元测试。`ui.test.cjs`、`pane-swap.test.cjs`、`scroll.test.cjs` 等浏览器脚本依赖实际服务、鉴权和会话环境，使用前需要按自己的环境调整。
