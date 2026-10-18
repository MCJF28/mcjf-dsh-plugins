# DSH 插件集

<a id="chinese"></a>

**中文** | [English](#english)

一套用于 [DeepSeek Harness](https://github.com/deepseek-ai) 桌面版的插件。每个独立成仓库、独立安装 —— 只取你需要的即可。

## 插件一览

| 插件 | 作用 |
|---|---|
| [dsh-memory-system-prompt](https://github.com/MCJF28/dsh-memory-system-prompt) | 全局记忆（AI 主动写入与读取）+ 用户级系统提示词。索引每轮注入但不占上下文。 |
| [dsh-web-search-router](https://github.com/MCJF28/dsh-web-search-router) | 按模型通道分流搜索：官方账号走 DeepSeek 官方搜索，其它通道走你的自建服务。失败时给出可读原因，而不是一句 500。 |
| [dsh-visual-card](https://github.com/MCJF28/dsh-visual-card) | AI 交一段 HTML，在对话里渲染成可交互卡片 —— 能点、能键盘操作、能全屏、能导出。 |
| [dsh-prompt-enhancer](https://github.com/MCJF28/dsh-prompt-enhancer) | 发送键旁一个按钮，把草稿改写成更好的提示词。三档力度，跟随当前对话的模型。 |

## 安装

**推荐：内置插件安装程序。** 打开「设置 → 内置插件」，粘贴包名，点安装，再重启应用：

```
dsh-visual-card
```

安装程序会自动写进 `dsh.profile.bundles`，不用手改任何文件。

命令行方式（先完全退出应用）：

```bash
cd ~/.dsh/profiles/desktop
pnpm add dsh-visual-card
```

然后把包名加进 `dsh.profile.bundles`，重启应用。

> 四个包都已发布到 npm，当前版本 `1.0.0`。

## 共同的取舍

这几个插件针对同一版 Harness 编写，有几处一致的判断：

- **Host 与 Client 分开。** 凡是涉及模型可见状态的（工具、路由、提示词装配）都在 `index.js` 里跑在 Host；用户看得见的在 `client.js` 里填槽位。改 Host 要重启，改 Client 通常刷新页面即可。
- **填槽位，不改造。** 都不修改宿主原有界面，只往宿主已经渲染的槽位里注册内容，所以 Harness 升级不会悄悄把它们弄坏。
- **失败要说清楚。** 配置不对时，提示直接指出该去改哪个设置，而不是甩一段堆栈。
- **设置在 `~/.dsh/` 下。** 每个插件各占一个目录，卸载包不会删数据，重装后自动接上。

## 许可

MIT，各仓库内有独立副本。

---

<a id="english"></a>

**English** | [中文](#chinese)

A set of plugins for [DeepSeek Harness](https://github.com/deepseek-ai) Desktop. Each lives in its own repository and installs independently — take only the ones you want.

## The plugins

| Plugin | What it does |
|---|---|
| [dsh-memory-system-prompt](https://github.com/MCJF28/dsh-memory-system-prompt) | Global memory the model writes and reads itself, plus a user-level system prompt. The index is injected every turn without consuming context. |
| [dsh-web-search-router](https://github.com/MCJF28/dsh-web-search-router) | Routes search by model channel: official DeepSeek search on account routes, your own endpoint elsewhere. Readable failure reasons instead of a bare 500. |
| [dsh-visual-card](https://github.com/MCJF28/dsh-visual-card) | The model hands over HTML and it renders as an interactive card in the conversation — clickable, keyboard-operable, fullscreen, exportable. |
| [dsh-prompt-enhancer](https://github.com/MCJF28/dsh-prompt-enhancer) | One button next to the send key rewrites your draft into a better prompt. Three levels, follows the model you are chatting with. |

## Install

**The built-in plugin installer is the recommended way.** Open Settings → Built-in Plugins, paste the package name, press install, then restart the app:

```
dsh-visual-card
```

The installer writes the entry into `dsh.profile.bundles` for you; no manual file edits.

From the command line (quit the app completely first):

```bash
cd ~/.dsh/profiles/desktop
pnpm add dsh-visual-card
```

Add the package name to `dsh.profile.bundles` and restart the app.

> All four packages are published to npm at `1.0.0`.

## Common ground

These plugins were built against the same Harness and share a few deliberate decisions:

- **Host versus client split.** Anything that touches model-visible state (tools, routing, prompt assembly) runs in `index.js` on the host; anything the user sees runs in `client.js` and fills a slot. Host changes need a restart, client changes usually just a page refresh.
- **Slots, not forks.** None of them modify the shipped UI. They register into slots the host already renders, so a Harness update cannot silently break them.
- **Readable failures.** When something is misconfigured, the message names the setting to fix, rather than surfacing a stack trace.
- **Settings live in `~/.dsh/`.** Each plugin keeps its own directory there, so uninstalling the package leaves the data behind and reinstalling picks it up again.

## License

MIT. See each repository for its own copy.
