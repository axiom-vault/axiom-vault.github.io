# Architecture

AxiomVault is split into a CLI and a shared Rust core.

## Repositories in this workspace

### `axiom-cli`

The CLI provides the user-facing commands for:

- Creating and opening vaults
- Adding and extracting files
- Authenticating remotes
- Running sync
- Mounting vaults over FUSE or WebDAV

### `axiom-core`

The shared Rust workspace contains the underlying implementation.

| Crate | Responsibility |
| --- | --- |
| `core/crypto` | Encryption, key derivation, streaming protection |
| `core/vault` | Vault engine, config, tree index, sessions |
| `core/storage` | Storage abstraction and providers |
| `core/sync` | Sync engine and conflict handling |
| `core/app` | App service layer and DTOs |
| `core/ffi` | C-compatible bindings for mobile clients |
| `core/fuse` | FUSE virtual filesystem |
| `core/webdav` | WebDAV server |
| `core/common` | Shared types and errors |

## Design goals

- Encrypt locally before remote storage
- Keep the system zero-knowledge
- Support multiple clients through a reusable core
- Separate transport and storage logic from vault semantics
