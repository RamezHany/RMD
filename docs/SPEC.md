# RMD — Product & Build Spec

**Name:** RMD · **Type:** open-source project · **Decided 2026-11-13:** the name is RMD, and it is built with **Rust**.

## The product in one line

A cross-platform (Windows / macOS / Linux) Markdown editor and viewer specialized in README files, with a built-in mini model that runs fully offline and helps design and format the document. Not a general-purpose editor — an editor with an opinion.

## Why Rust — Tauri

- ~10 MB app size instead of Electron's ~150 MB.
- The native WebView renders HTML and SVG exactly like a browser — a hard requirement for faithful README preview (badges, shields).
- A Rust core: safety and speed for file handling, plus direct llama.cpp bindings for local model inference.
- The name works in the terminal: `rmd file.md`.

## Stack

- **Shell:** Tauri 2 (Rust)
- **UI:** TypeScript + React + CodeMirror 6
- **Markdown rendering:** pulldown-cmark (Rust) + ammonia sanitization → safe preview HTML
- **File watching:** the `notify` crate — live preview refresh on external changes
- **Model:** llama.cpp via llama-cpp-2 bindings — Qwen2.5-Coder-1.5B in GGUF (Q4 ≈ 1 GB), CPU-only, 100% offline
- **Fine-tuning:** LoRA on (plain README → designed README) pairs

## v1 scope — what actually gets built

**Viewer:** open any `.md` file and render it the way GitHub does (SVG badges, relative images, tables, syntax highlighting), plus a table of contents and light/dark themes.

**Editor:** split-view editing with live preview, autosave, and opening files from the terminal.

**Assistant:** suggestions at the level of a **single section only** — the user sees a diff and accepts or rejects it. The model never writes the whole file.

**Out of scope (later):** collaboration, cloud sync, a plugin system, mobile.

## Build phases

0. Tauri scaffold + a window that opens a file.
1. Viewer: rendering + TOC + themes.
2. Editor: CodeMirror + live preview + autosave.
3. Model integration: local inference + suggestions UI with diffs.
4. Fine-tune: dataset + LoRA + evaluation, then the v0.1 release.

## Hard rules

- The model is **always offline** — the assistant makes no network calls, ever.
- **Performance before decoration:** opening a 1 MB file in under a second is a fixed target.
