# DSH 插件集

[English](./README.md) | 中文

一套用于 [DeepSeek Harness](https://github.com/deepseek-ai) 桌面版的插件。每个独立成仓库、独立安装 —— 只取你需要的即可。

## 插件一览

| 插件 | 作用 |
|---|---|
| [dsh-memory-system-prompt](https://github.com/MCJF28/dsh-memory-system-prompt) | 全局记忆（AI 主动写入与读取）+ 用户级系统提示词。索引每轮注入但不占上下文。 |
| [dsh-web-search-router](https://github.com/MCJF28/dsh-web-search-router) | 按模型通道分流搜索：官方账号走 DeepSeek 官方搜索，其它通道走你的自建服务。失败时给出可读原因，而不是一句 500。 |
| [dsh-visual-card](https://github.com/MCJF28/dsh-visual-card) | AI 交一段 HTML，在对话里渲染成可交互卡片 —— 能点、能键盘操作、能全屏、能导出。 |
| [dsh-prompt-optimizer](https://github.com/MCJF28/dsh-prompt-optimizer) | 发送键旁一个按钮，把草稿改写成更好的提示词。三档力度，跟随当前对话的模型。 |

## 安装

**先完全退出应用。** 运行中安装会因为文件被锁而写出残缺的包。

```bash
cd ~/.dsh/profiles/desktop

# 锁版本安装，不要跟 main
pnpm add github:MCJF28/dsh-visual-card#v1.0.0
```

然后把包名加进 profile `package.json` 的 `dsh.profile.bundles`：

```json
{
  "dsh": {
    "profile": {
      "bundles": ["dsh-visual-card"]
    }
  }
}
```

重启应用。每个插件都要单独走一次这两步。

> 用 GitHub 地址安装意味着这些包不在 npm 上。可用版本就是各仓库的 tag —— 目前是 `v1.0.0`。

## 共同的取舍

这几个插件针对同一版 Harness 编写，有几处一致的判断：

- **Host 与 Client 分开。** 凡是涉及模型可见状态的（工具、路由、提示词装配）都在 `index.js` 里跑在 Host；用户看得见的在 `client.js` 里填槽位。改 Host 要重启，改 Client 通常刷新页面即可。
- **填槽位，不改造。** 都不修改宿主原有界面，只往宿主已经渲染的槽位里注册内容，所以 Harness 升级不会悄悄把它们弄坏。
- **失败要说清楚。** 配置不对时，提示直接指出该去改哪个设置，而不是甩一段堆栈。
- **设置在 `~/.dsh/` 下。** 每个插件各占一个目录，卸载包不会删数据，重装后自动接上。

## 许可

MIT，各仓库内有独立副本。
