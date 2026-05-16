# AxiomVault

> Private files first. Cloud sync second.

AxiomVault is an **encrypted vault** for people who want local-first control with optional cloud sync.
It is built around **client-side encryption**, a **zero-knowledge design goal**, and a CLI-first workflow that can grow into desktop and mobile clients over time.

## What AxiomVault is trying to be

AxiomVault aims to make a simple promise:

1. encrypt data on your device
2. keep cloud providers unaware of plaintext contents
3. let you move the same vault across machines without changing how it works

Today, the docs describe an **early-development** implementation centered on `axiom-cli` and the shared `axiom-core` Rust workspace.

## Product snapshot

| Area | Current direction |
| --- | --- |
| Primary interface | CLI-driven vault management |
| Encryption model | Client-side encryption before sync |
| Recovery model | Password + recovery mnemonic wrapping the same master key |
| Remote backends today | Google Drive, local filesystem |
| Access layers | Native vault commands, optional FUSE mount, optional WebDAV |
| MCP support | Not implemented or documented in this repo today |
| Hardware-key support | Not implemented or documented in this repo today |
| Project maturity | Early development, not production ready |

## Why it exists

- **Private by default** — data is encrypted before it leaves your machine.
- **Local-first workflow** — the vault remains useful even without a cloud connection.
- **Composable architecture** — the same core is intended to serve CLI, sync, mount, and future client surfaces.
- **Portable model** — a vault should be understandable as a product, not tied to one storage vendor.

## Start here

- [Quickstart](quickstart.md) — create a vault, add a file, and run a first sync.
- [Security](security.md) — review the crypto model, trust assumptions, and safeguards.
- [Threat Model](threat-model.md) — see which attackers and boundaries the design focuses on.
- [Current Limitations](current-limitations.md) — understand what is incomplete or risky today.
- [MCP Status](mcp-status.md) — see what MCP-related automation is and is not available today.
- [YubiKey and Hardware Keys](yubikey-and-hardware-keys.md) — see the current lack of hardware-key integration claims.
- [Architecture](architecture.md) — understand how `axiom-cli` and `axiom-core` fit together.
- [Sync and Cloud](sync-and-cloud.md) — review current backend support and sync behavior.

## Main capabilities in scope

- Local encryption before data touches cloud storage
- Vault lifecycle management from the CLI
- Encrypted file storage with a tree index
- Sync engine with conflict handling strategies
- Optional FUSE mount and WebDAV access layers
- Shared Rust core intended for reuse across clients
- No documented MCP integration today
- No documented YubiKey or hardware-key workflow today

## Repository components

- `axiom-cli` — commands for creating, opening, mounting, and syncing vaults.
- `axiom-core` — shared Rust crates for crypto, storage, sync, FFI, WebDAV, and FUSE.

## Current status

> AxiomVault is in **early development**.
> Expect rough edges, format changes, incomplete hardening, and missing operational polish.
> These docs should help contributors and evaluators understand the direction of the project, not treat it as production-ready security guidance.
