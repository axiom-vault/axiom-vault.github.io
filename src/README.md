# AxiomVault

AxiomVault is a cross-platform encrypted vault built around **client-side encryption** and a **zero-knowledge** design.

## Start here

- [Quickstart](quickstart.md) — install the CLI, create a vault, add a file, and run your first sync.
- [Security](security.md) — review the encryption model, key handling, and readiness caveats.
- [CLI Usage](cli.md) — learn the main `axiom` commands for vaults, files, remotes, mounts, and sync.
- [Architecture](architecture.md) — understand how `axiom-cli` and `axiom-core` fit together.

## What this workspace contains

- `axiom-cli` — command-line interface for creating, opening, mounting, and syncing vaults.
- `axiom-core` — shared Rust library for encryption, storage, sync, FFI, WebDAV, and FUSE.

## Current status

> This project is in early development and is **not production ready** yet.

Use these docs as a starting point for internal documentation, contributor onboarding, and future public product docs.

## Main capabilities

- Local encryption before data touches cloud storage
- Vault lifecycle management from the CLI
- Google Drive remote support
- Sync engine with conflict resolution strategies
- Optional FUSE mount and WebDAV access layers
