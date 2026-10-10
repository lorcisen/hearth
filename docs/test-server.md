# Test server setup (home lab)

Hearth is developed against a local Hyper-V VM so we can snapshot and reset to a clean OS at will
(HestiaCP requires a fresh server).

## VM

1. Enable **Hyper-V** (Settings → System → Optional features → More Windows features → Hyper-V), reboot.
2. Hyper-V Manager → Virtual Switch Manager → create an **External** switch (VM gets a LAN IP).
3. New VM: Generation 2, **2 vCPU, 4 GB RAM, 40 GB disk**. Secure Boot template: *Microsoft UEFI Certificate Authority*.
4. Install **Ubuntu Server 24.04 LTS**:
   - Select **only** "Install OpenSSH server".
   - Do **not** select any featured snaps (especially not Docker).
   - Create a normal user with sudo.
5. Reserve a fixed IP for the VM in the router (DHCP reservation).
6. Verify from Windows: `ssh <user>@<ip>`.
7. Take checkpoint **`clean-install`**.

Later checkpoints: **`hestia-installed`** (after HestiaCP install).

## Domain

- Test domain: **burken.stream** (on Cloudflare). Use it freely for experiments — not production.
- The server is behind NAT, so certificates use **Cloudflare Tunnel** or **DNS-01** validation; no port forwarding needed.

## Rules

- Never develop/test against production servers.
- Revert to `clean-install` before testing installer flows.
