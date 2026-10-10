# Hearth

**A Windows desktop app for installing and managing Linux servers — HestiaCP, Docker, Cloudflare and more, from one place.**

> 🚧 **Status: planning / early development.** Nothing usable yet. See [docs/DEVLOG.md](docs/DEVLOG.md) for progress.

Hearth connects to your servers over SSH (no agent required) and gives you a friendly GUI for the
things you normally do by hand in a terminal: hardening a fresh server, installing HestiaCP and Docker,
creating websites, pointing domains through Cloudflare, watching resources, and taking backups.
Every action shows the exact commands it runs, and config changes can be undone.

## Planned features

- **Servers** — add via SSH key/password, groups & tags, jump hosts, hardening wizard, create VPS via provider APIs
- **HestiaCP** — install on a clean server, web domains, SSL (Let's Encrypt), databases, mail, users, backups
- **Docker** — containers, images, volumes, networks, live logs, compose stacks, image update checks; apps exposed through Hestia proxy templates
- **App catalog** — one-click templates (WordPress, Nextcloud, Uptime Kuma, Gitea, n8n, Vaultwarden, …)
- **Cloudflare** — zones, DNS records, proxy toggle, SSL mode, cache purge, Cloudflare Tunnel, DNS-01 certificates
- **Monitoring & alerts** — CPU/RAM/disk, services, uptime checks, SSL/domain expiry, notifications (Windows, email, Discord, Telegram, Slack)
- **Backups** — scheduled, to B2 / R2 / S3 / local, with restore and verification
- **Security** — firewall & fail2ban GUI, security score with one-click fixes, SSH key management
- **Tools** — tabbed SSH terminal, SFTP file manager with editor, log viewer, cron editor
- **Recipes** — reusable parameterised YAML playbooks, run on one or many servers
- **Change history** — timeline of everything Hearth did, with undo
- **Bulk actions**, **dry-run mode**, **health reports**, **export as code** (compose / Ansible)
- **AI assistant** (opt-in, bring your own Claude API key) — explain errors, suggest fixes, plain-language tasks; nothing runs without your approval

## Target platforms

- **Client:** Windows 10/11
- **Servers:** Ubuntu 22.04/24.04 and Debian 12 (more later)

## Tech stack

Tauri 2 (Rust) · React + TypeScript · xterm.js · Monaco Editor

## Architecture

Hearth is built to be modular: a small **core** (SSH, job runner, secrets vault, change history, event bus)
plus **provider interfaces** (web panel, DNS, backup storage, VPS) and self-contained **modules**.
See [docs/decisions](docs/decisions) for the reasoning behind key choices.

## License

[MIT](LICENSE)
