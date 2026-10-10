# 0001 — Tauri 2 + React/TypeScript

- **Date:** 2026-10-10
- **Status:** Accepted

## Context
Hearth is a Windows desktop app that needs an embedded terminal, a code editor, rich dashboards,
and a backend capable of SSH, encryption and background jobs.

## Decision
Use **Tauri 2** (Rust backend) with a **React + TypeScript** frontend. Terminal via **xterm.js**, editor via **Monaco**.

## Alternatives
- **.NET 9 + Avalonia/WinUI 3** — mature SSH.NET library, but terminal/editor components are weaker than xterm.js/Monaco.
- **Electron** — same web UI benefits, but much larger binaries and memory use.

## Consequences
- Small installer, native WebView2, strong typing end to end.
- Rust SSH stack (`russh`) and crypto must be learned/maintained.
- Cross-platform (macOS/Linux client) becomes possible later at low cost.
