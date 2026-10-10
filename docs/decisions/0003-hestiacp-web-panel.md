# 0003 — HestiaCP as the first web panel provider

- **Date:** 2026-10-10
- **Status:** Accepted

## Context
The maintainer already runs HestiaCP. Writing our own Nginx/PHP/SSL/mail/database management is a large effort
that HestiaCP already solves, and it exposes a full CLI (`v-*` commands) and an API.

## Decision
Web hosting features (web domains, SSL, databases, mail, users, backups) are implemented as a
**HestiaCP provider** that drives Hestia's CLI over SSH (API support may follow).

## Consequences / constraints
- HestiaCP must be installed on a **clean** server → Hearth's installer must detect and warn about existing software.
- Hestia owns ports 80/443 → Docker apps are exposed via **custom Hestia Nginx proxy templates**, never by binding 80/443.
- Hestia ships its own firewall (iptables) and fail2ban → hardening on Hestia servers uses **Hestia's firewall**, not UFW.
- Hestia's built-in DNS server is not used for public DNS; **Cloudflare** is the DNS provider.
- **Mail** is in scope (user uses Hestia mail) → Cloudflare module must create MX/SPF/DKIM/DMARC records (DNS-only, not proxied).
- Other web panel providers (plain Nginx, Caddy) can be added later behind the same interface.
