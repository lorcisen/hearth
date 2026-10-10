# 0002 — Agentless management over SSH

- **Date:** 2026-10-10
- **Status:** Accepted

## Context
Users should be able to manage a server the moment it has SSH, without installing anything first.

## Decision
All management happens over **SSH** (commands + SFTP). No server-side agent is required.
An **optional** lightweight agent may be added later for real-time metrics and push alerts.

## Consequences
- Zero footprint on servers; works on any Ubuntu/Debian box with SSH.
- Monitoring is poll-based while Hearth is running (until the optional agent exists).
- Every action maps to visible shell commands → enables "show commands" transparency and dry-run.
