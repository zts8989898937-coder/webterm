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

本仓库为**脱敏公开版**，`server.js` 中的默认口令占位符需通过环境变量 `WEBTERM_PASS` 注入，请勿将真实凭据提交到版本库。
