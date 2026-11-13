# Contributing to RMD

Thanks for your interest. RMD is in **pre-alpha** (spec stage), so the most valuable contributions right now are ideas, issues, and discussion.

## How work flows here

1. **Issues first.** Open an issue describing the problem or idea before writing code.
2. **One branch per issue** (`fix/...`, `feat/...`, `docs/...`). Never commit directly to `main`.
3. **Conventional Commits** — `fix: ...`, `feat: ...`, `docs: ...`, `chore: ...`.
4. **Pull requests with evidence.** Link the issue (`Closes #N`) and show how you verified the change.
5. **Reviews are the maintainer's.** PRs stay open until reviewed — please don't expect instant merges, and never force-push after a review starts.

## Development setup (once the scaffold lands)

- Rust (stable) — https://rustup.rs
- Node.js 20+
- Tauri 2 prerequisites for your OS — https://tauri.app/start/prerequisites/

```bash
git clone https://github.com/RamezHany/RMD.git
cd RMD
npm install
npm run tauri dev
```

## Ground rules

- The assistant model is **offline-only** — contributions must not add network calls to it.
- Model weights (`*.gguf`) are never committed; they are downloaded or built locally.
- Performance is a feature: opening a 1 MB Markdown file must stay under one second.
