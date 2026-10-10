# 0004 — Core + providers + modules

- **Date:** 2026-10-10
- **Status:** Accepted

## Context
The feature list is long and will keep growing. New features must be addable without touching the core.

## Decision
Three layers:

1. **Core** — SSH sessions, job runner (with dry-run + command transcript), secrets vault (Windows DPAPI),
   change history (snapshots + undo), event bus, settings, i18n.
2. **Provider interfaces** — swappable implementations behind a trait:
   - `WebPanelProvider` (HestiaCP first)
   - `DnsProvider` (Cloudflare first)
   - `BackupStorage` (B2 / R2 / S3 / local)
   - `VpsProvider` (Hetzner / DigitalOcean / Vultr)
   - `Notifier` (Windows, email, Discord, Telegram, Slack)
   - `IngressProvider` (Direct / Cloudflare Tunnel / VPN) — added by [ADR 0006](0006-networking-ingress.md)
3. **Modules** — self-contained features (Docker, Monitoring, Security, Recipes, AI, Reports, …).
   Each module has a manifest, its own Rust commands and its own frontend routes/pages,
   and registers itself in one place. Removing a module must not break the core.

Recipes are **declarative YAML**, so new automation can be shared without writing code.

## Consequences
- Slightly more upfront design work on interfaces.
- Clear boundaries make contributions and testing easier.
