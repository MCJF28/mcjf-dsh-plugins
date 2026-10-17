# DSH Plugins

English | [中文](./README.zh.md)

A set of plugins for [DeepSeek Harness](https://github.com/deepseek-ai) Desktop. Each lives in its own repository and installs independently — take only the ones you want.

## The plugins

| Plugin | What it does |
|---|---|
| [dsh-memory-system-prompt](https://github.com/MCJF28/dsh-memory-system-prompt) | Global memory the model writes and reads itself, plus a user-level system prompt. The index is injected every turn without consuming context. |
| [dsh-web-search-router](https://github.com/MCJF28/dsh-web-search-router) | Routes search by model channel: official DeepSeek search on account routes, your own endpoint elsewhere. Readable failure reasons instead of a bare 500. |
| [dsh-visual-card](https://github.com/MCJF28/dsh-visual-card) | The model hands over HTML and it renders as an interactive card in the conversation — clickable, keyboard-operable, fullscreen, exportable. |
| [dsh-prompt-optimizer](https://github.com/MCJF28/dsh-prompt-optimizer) | One button next to the send key rewrites your draft into a better prompt. Three levels, follows the model you are chatting with. |

## Install

**Quit the app first.** Installing while it runs writes a half-finished package, because the files are locked.

```bash
cd ~/.dsh/profiles/desktop

# Pin a version rather than following main
pnpm add github:MCJF28/dsh-visual-card#v1.0.0
```

Then add the package name to `dsh.profile.bundles` in the profile's `package.json`:

```json
{
  "dsh": {
    "profile": {
      "bundles": ["dsh-visual-card"]
    }
  }
}
```

Restart the app. Each plugin needs this step separately.

> Requiring a GitHub specifier means the package is not on npm. Available versions are the tags in each repository — currently `v1.0.0`.

## Common ground

These plugins were built against the same Harness and share a few deliberate decisions:

- **Host versus client split.** Anything that touches model-visible state (tools, routing, prompt assembly) runs in `index.js` on the host; anything the user sees runs in `client.js` and fills a slot. Host changes need a restart, client changes usually just a page refresh.
- **Slots, not forks.** None of them modify the shipped UI. They register into slots the host already renders, so a Harness update cannot silently break them.
- **Readable failures.** When something is misconfigured, the message names the setting to fix, rather than surfacing a stack trace.
- **Settings live in `~/.dsh/`.** Each plugin keeps its own directory there, so uninstalling the package leaves the data behind and reinstalling picks it up again.

## License

MIT. See each repository for its own copy.
