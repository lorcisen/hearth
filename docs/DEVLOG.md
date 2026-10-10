# Development Log

Running log of everything done in this project — newest entry first.
Each entry: what was done, why, files touched, next step.

---

## 2026-10-10 — Test server: physical ThinkCentre instead of Hyper-V

**Decision**
- Test server is a dedicated **Lenovo ThinkCentre** (not a Hyper-V VM).
- No snapshots on bare metal → clean state restored via **Clonezilla** disk images (`clean-install`, `hestia-installed`) or reinstall.

**Files**
- `docs/test-server.md` (rewritten: hardware, BIOS settings, USB install, Clonezilla)
- `docs/DEVLOG.md` (updated)

---

## 2026-10-10 — Name, repository & project docs

**Decisions**
- Project name: **Hearth** (Hestia = goddess of the hearth). Checked: `lorcisen/hearth` was free, no notable server tool with that name.
- **HestiaCP mail is in scope** → Cloudflare module must handle MX/SPF/DKIM/DMARC (DNS-only records).
- Test domain: **burken.stream** (Cloudflare). Test server: Hyper-V VM, Ubuntu Server 24.04.

**Done**
- `git init`, created public GitHub repo **lorcisen/hearth**, initial commit pushed.
- Wrote README, MIT LICENSE, CHANGELOG, .gitignore, .gitattributes.
- Wrote ADRs 0001–0005 (Tauri, agentless SSH, HestiaCP, modular architecture, MIT).
- Wrote `docs/test-server.md` (Hyper-V VM setup + rules).

**Files**
- `README.md`, `LICENSE`, `CHANGELOG.md`, `.gitignore`, `.gitattributes` (new)
- `docs/test-server.md`, `docs/decisions/*` (new)
- `docs/DEVLOG.md` (updated)

**Next**
- User: set up Hyper-V test VM per `docs/test-server.md`.
- Claude: write detailed v0.1 plan (`docs/plan-v0.1.md`) for approval.

---

## 2026-10-10 — Planning & dev environment

**Decisions (from planning discussion)**
- Open source, **MIT** license, **English** project name (TBD).
- Stack: **Tauri 2 (Rust) + React/TypeScript**, xterm.js (terminal), Monaco (editor).
- Web panel: **HestiaCP** (user already runs it on Ubuntu 22.04).
- Target distros: **Ubuntu / Debian** first.
- All extra ideas included: recipes/playbooks, change history with undo, bulk actions,
  AI assistant (Claude API, opt-in), health reports, export-as-code, dry-run.
- Architecture must be **modular** (core + provider interfaces + modules).
- Logging: git commits + this DEVLOG + CHANGELOG.md + `docs/decisions/` (ADRs).

**Done**
- Checked prerequisites: Git 2.55, Node 24.14, gh 2.102, VS Build Tools 2019 (MSVC), WebView2 154 — present.
- Installed **Rust** via winget (`Rustlang.Rustup` 1.29.1) → rustc/cargo 1.99.0, toolchain `stable-x86_64-pc-windows-msvc`.
- Installed **pnpm** 12.10.1 (`npm install -g pnpm`).
- Created this log.

**Files**
- `docs/DEVLOG.md` (new)

**Next**
- Choose project name, `git init`, create GitHub repo.
- User sets up a home test server (see setup notes in chat / to be added to `docs/test-server.md`).
- Write detailed v0.1 plan for approval.
