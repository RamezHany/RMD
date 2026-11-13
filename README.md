# RMD

**A Markdown editor & viewer with taste — built for READMEs.**

RMD is a cross-platform (Windows · macOS · Linux) Markdown editor and viewer with a built-in, fully offline mini model that helps you *design* your documents — badges, headers, tables, layout — instead of just typing them.

> 🚧 **Status: pre-alpha.** The product spec is final (see [docs/SPEC.md](docs/SPEC.md)); the build has not started yet. Watch the repo if you want to follow along.

## Why RMD?

- **GitHub-faithful preview.** What you see is what GitHub renders — SVG badges, shields, relative images, tables, syntax highlighting.
- **An assistant that only suggests.** The built-in model proposes changes **one section at a time**, presented as a diff you accept or reject. It never rewrites your whole file.
- **100% offline.** The model runs locally on CPU. No accounts, no cloud, no telemetry — your files never leave your machine.
- **Fast and small.** A Rust core with a native webview: a ~10 MB app, and a 1 MB file opens in under a second.

## Stack

| Layer | Choice |
|---|---|
| App shell | Tauri 2 (Rust) |
| UI | TypeScript · React · CodeMirror 6 |
| Rendering | pulldown-cmark + ammonia (sanitized HTML) |
| File watching | notify |
| AI model | llama.cpp · Qwen2.5-Coder-1.5B (GGUF, Q4) — LoRA fine-tuned on README design pairs |

## Roadmap

- [ ] **Phase 0** — Tauri scaffold; open a file from the terminal: `rmd file.md`
- [ ] **Phase 1** — Viewer: GitHub-style rendering, table of contents, light/dark themes
- [ ] **Phase 2** — Editor: split live preview, autosave
- [ ] **Phase 3** — Local model: section-level suggestions with a diff view
- [ ] **Phase 4** — LoRA fine-tune + v0.1 release

Full details: [docs/SPEC.md](docs/SPEC.md)

## Design principles

1. **Offline, always.** The assistant makes zero network calls.
2. **Suggestions, not takeovers.** Section-by-section diffs; the human decides.
3. **Performance before decoration.** If it isn't fast, it doesn't ship.

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md). Short version: open an issue first, branch per issue, Conventional Commits, and pull requests stay unmerged until reviewed.

## License

[Apache-2.0](LICENSE) © Ramez Hany
