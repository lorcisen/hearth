# 0006 — Networking module & ingress providers

- **Date:** 2026-10-10
- **Status:** Accepted

## Context
Not every server has a public IP. The maintainer's test server is on **5G mobile data behind CGNAT**
and gets a public IPv4 (all ports open) through **OVPN.com** (Swedish VPN with a public IPv4 add-on), via OpenVPN.

Traffic types have different needs:

| Traffic | Needs public IP? | Solution |
|---|---|---|
| Hearth → server (SSH) | No | LAN IP when at home |
| Websites (HTTP/S) | No | Cloudflare Tunnel (outbound connection, works behind CGNAT) |
| Mail (SMTP 25, IMAP, …) | **Yes** | Public IP via VPN (Tunnel cannot carry SMTP) |

## Decision
Add a **Networking module** and an `IngressProvider` interface describing how outside traffic reaches a server:

- `Direct` — server has its own public IP.
- `CloudflareTunnel` — `cloudflared` on the server, outbound only.
- `Vpn` — public IP through a VPN (OpenVPN first, WireGuard later).

Networking module features:
- Upload `.ovpn` → install OpenVPN, run as systemd service (`openvpn-client@`), auto-start.
- **Split routing / LAN protection**: LAN and local SSH must keep working when the tunnel is up
  (default OpenVPN redirects all traffic and can lock Hearth out). Always verify LAN SSH after changes, auto-rollback on failure.
- Health check: tunnel status + current public IP.
- **DDNS**: update Cloudflare A records automatically when the public IP changes.
- **Mail readiness check**: port 25 reachability (in/out), DNS blacklists, PTR/rDNS match.
- Optional **SMTP relay** setup in Hestia (Brevo/Mailgun/SES) for outgoing mail, since VPN IPs often have poor mail reputation.
- "New site" wizard asks which ingress to use.

## Consequences
- Scheduled for **v0.3** together with Cloudflare Tunnel; v0.1 development works over LAN + Tunnel without a VPN.
- Hestia firewall rules must account for the VPN interface (`tun0`).
