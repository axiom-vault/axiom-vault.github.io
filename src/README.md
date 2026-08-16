# AxiomVault

> Private files first. Cloud sync second.

AxiomVault is an early-development encrypted-vault project built around client-side encryption and a CLI-first workflow. Its zero-knowledge and multi-device behavior are **design goals**, not complete guarantees.

## Status vocabulary

Every capability statement in this book uses one of these labels:

- **available** — implemented on the referenced default-branch revision; this is not a production-readiness claim.
- **experimental-incomplete** — runnable, but a known correctness, security, or durability boundary is incomplete.
- **scaffolded** — an API, command, or component exists, but the end-to-end behavior is not operationally verified.
- **unavailable** — no verified implementation provides the behavior.

The status below was checked against [`axiom-core@b6520ff`](https://github.com/axiom-vault/axiom-core/commit/b6520ff6e453cc1c2a74d78c25f11a35ec75408c) and [`axiom-cli@7b436af`](https://github.com/axiom-vault/axiom-cli/commit/7b436aff5a8d5236d075a9e2bfe7f998d171b83c), the current default-branch revisions reviewed for this update. The CLI pins an older core revision, so a fix on `axiom-core/main` is not a CLI fix until the pin is updated and compatibility is tested ([CLI #25](https://github.com/axiom-vault/axiom-cli/issues/25)). These labels do not claim that open fixes are shipped or released.

## Current capability snapshot

| Capability | Status | Current boundary |
| --- | --- | --- |
| Local CLI vault lifecycle and file commands | **available** | Early-development format and operational hardening still apply. |
| Local and Google Drive storage providers | **experimental-incomplete** | Google Drive OAuth credentials can enter portable provider configuration; see [Sync and Cloud](sync-and-cloud.md). |
| Multi-device sync convergence | **experimental-incomplete** | Remote downloads are not persisted before sync state can advance ([core #15](https://github.com/axiom-vault/axiom-core/issues/15)). |
| Periodic/background sync | **scaffolded** | Configuration and scheduler types exist; the CLI is not a verified background-sync service. |
| Bounded-memory streaming | **unavailable** | Chunk primitives exist, but file paths buffer complete data ([core #18](https://github.com/axiom-vault/axiom-core/issues/18)). |
| FUSE mount | **experimental-incomplete** | Optional build/platform feature with an expanded plaintext access surface. |
| WebDAV mount | **experimental-incomplete** | CLI binds to IPv4 loopback, but requests are unauthenticated and core does not enforce loopback ([core #12](https://github.com/axiom-vault/axiom-core/issues/12), [CLI #23](https://github.com/axiom-vault/axiom-cli/issues/23)). |
| Snapshot rollback detection / trusted freshness | **unavailable** | AEAD integrity does not detect replay of an older valid snapshot ([core #13](https://github.com/axiom-vault/axiom-core/issues/13)). |
| MCP workflow | **unavailable** | No supported MCP workflow is documented here. |

## Start here

- [Quickstart](quickstart.md) — exercise verified local CLI commands.
- [Security](security.md) — review implemented protections and incomplete boundaries.
- [Threat Model](threat-model.md) — see attacker and trust assumptions.
- [Current Limitations](current-limitations.md) — review the known gaps before experimenting.
- [Architecture](architecture.md) — understand how the CLI and core fit together.
- [Sync and Cloud](sync-and-cloud.md) — review provider, sync, and credential status.
- [MCP Status](mcp-status.md) and [YubiKey and Hardware Keys](yubikey-and-hardware-keys.md) — feature-specific status pages.

## Repository components

- `axiom-cli` — the command surface for local vaults, remotes, sync, and mounts.
- `axiom-core` — shared Rust crates for crypto, vault, storage, sync, FFI, WebDAV, and FUSE.

> AxiomVault is **not production ready**. Use non-critical data only, expect format changes, and verify the exact revision you run.
