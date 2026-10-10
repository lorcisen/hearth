# Test server setup (home lab)

Hearth is developed against a dedicated physical test machine at home: a **Lenovo ThinkCentre**
running Ubuntu Server. HestiaCP requires a fresh server, so we keep a way to quickly return to a clean OS.

## Hardware

- Lenovo ThinkCentre (any recent model is fine). Recommended: **≥ 4 GB RAM, ≥ 64 GB SSD**.
- Connect with **wired Ethernet** (more stable than Wi-Fi for a server).
- USB stick (≥ 4 GB) for the installer.

## BIOS (F1 at boot)

- **After Power Loss → Power On** — server comes back by itself after a power cut.
- **Wake on LAN → enabled** (optional, lets Hearth wake the machine later).
- Boot order: USB first during install. Secure Boot can stay on (Ubuntu supports it).

## Install Ubuntu Server 24.04 LTS

1. Download Ubuntu Server 24.04 LTS from ubuntu.com and write it to the USB stick
   with **Rufus** or **balenaEtcher**.
2. Boot the ThinkCentre from USB and install:
   - Use the **entire disk** (no LVM needed, default is fine).
   - Select **only** "Install OpenSSH server".
   - Do **not** select any featured snaps (especially not Docker) — Hearth installs everything.
   - Create a normal user with sudo.
3. Reserve a **fixed IP** for the machine in the router (DHCP reservation, use the MAC address of the Ethernet port).
4. Verify from Windows: `ssh <user>@<ip>`.
5. Run updates once: `sudo apt update && sudo apt full-upgrade -y && sudo reboot`.

Do **not** install HestiaCP, Docker or anything else by hand — testing Hearth's own installers is the point.

## Getting back to a clean state

A physical machine has no snapshots, so pick one of these:

- **Disk image (recommended):** after step 5, boot **Clonezilla** from USB and save an image of the disk
  (e.g. to a USB drive or a network share) named `clean-install`. Restoring takes a few minutes.
  Make a second image `hestia-installed` once HestiaCP is on.
- **Reinstall:** reinstall Ubuntu from the USB stick (~15–20 min).

## Connectivity

- Internet via **5G mobile data** → behind carrier NAT (CGNAT), no public IP of its own.
- Public IPv4 via **OVPN.com** (OpenVPN, public IPv4 add-on, all ports open) — needed for **mail**.
- Websites can use **Cloudflare Tunnel** instead and don't need the VPN.
- Hearth connects over the **LAN IP** while developing.
- ⚠️ Don't set up OpenVPN by hand yet — a default OpenVPN config routes *all* traffic through the tunnel and can
  cut off SSH from the LAN. Hearth's Networking module (v0.3) sets it up with split routing. See [ADR 0006](decisions/0006-networking-ingress.md).

## Domain

- Test domain: **burken.stream** (on Cloudflare). Use it freely for experiments — not production.
- The server is behind the home router (NAT), so certificates use **Cloudflare Tunnel** or **DNS-01**
  validation — no port forwarding needed.

## Rules

- Never develop/test against production servers.
- Restore `clean-install` before testing installer flows.
