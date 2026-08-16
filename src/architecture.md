# Architecture

AxiomVault is split into a CLI and a shared Rust core. Component existence does not imply that every end-to-end path is complete; statuses use the vocabulary defined on the [overview](README.md#status-vocabulary).

## Repositories and verified revisions

- [`axiom-cli@7b436af`](https://github.com/axiom-vault/axiom-cli/commit/7b436aff5a8d5236d075a9e2bfe7f998d171b83c) provides commands for vaults, files, remotes, sync, FUSE, and WebDAV.
- [`axiom-core@b6520ff`](https://github.com/axiom-vault/axiom-core/commit/b6520ff6e453cc1c2a74d78c25f11a35ec75408c) provides reusable implementation crates.
- The CLI currently pins an older core revision. Default-branch core work is not available through the CLI until the pin is updated and tested ([CLI #25](https://github.com/axiom-vault/axiom-cli/issues/25)).

## Component status

| Component | Role | Status and boundary |
| --- | --- | --- |
| `core/crypto` | Key derivation and authenticated encryption | **available** primitives; **unavailable** end-to-end bounded-memory streaming. Current stream code and higher layers buffer data ([core #18](https://github.com/axiom-vault/axiom-core/issues/18)). |
| `core/vault` | Config, encrypted tree, sessions, operations | **experimental-incomplete**: normal paths exist, but transactional mutation and freshness/rollback protections remain open ([core #14](https://github.com/axiom-vault/axiom-core/issues/14), [core #13](https://github.com/axiom-vault/axiom-core/issues/13)). |
| `core/storage` | Local and cloud provider abstraction | **experimental-incomplete**: providers exist, but portable configuration can include OAuth credentials ([core #11](https://github.com/axiom-vault/axiom-core/issues/11)). |
| `core/sync` | Diffing, ETags, strategies, scheduling types | **experimental-incomplete** for manual runs; **scaffolded** for background scheduling. Downloaded remote bytes are not durably applied ([core #15](https://github.com/axiom-vault/axiom-core/issues/15)). |
| `core/app` | Service layer, DTOs, optional local SQLite index | **experimental-incomplete**: the index contains plaintext metadata and its permission/wipe boundary is not fail-closed ([core #16](https://github.com/axiom-vault/axiom-core/issues/16)). |
| `core/ffi` | C-compatible client bindings | **experimental-incomplete**: legacy migration authentication, atomicity, and recovery output are open ([core #17](https://github.com/axiom-vault/axiom-core/issues/17)). |
| `core/fuse` | FUSE virtual filesystem | **experimental-incomplete** optional access layer. |
| `core/webdav` | HTTP/WebDAV access to an unlocked vault | **experimental-incomplete**: no per-request authentication and no core-enforced loopback restriction ([core #12](https://github.com/axiom-vault/axiom-core/issues/12)). |
| `axiom-cli` | User-facing command parser and orchestration | Local commands are **available**; cloud, sync, migration, import/export, and WebDAV inherit the boundaries above. |

## Important data paths

- CLI import/export and current core interfaces pass complete `Vec<u8>` values. “Chunked encryption” therefore does not mean bounded-memory streaming.
- The encrypted tree belongs to the portable vault. The optional app local index is a separate SQLite cache containing plaintext names, paths, sizes, and timestamps while in use.
- Remote provider configuration is portable. At the reviewed revisions, Google Drive token data is serialized into that configuration; credential locality is not enforced.
- Per-object authentication establishes integrity, not freshness. No trusted local monotonic anchor currently rejects a replayed, internally valid old snapshot.

## Design goals, not current guarantees

- Encrypt locally before remote storage.
- Keep cloud providers unaware of plaintext content and metadata.
- Converge safely across clients.
- Reuse the core across CLI and future client surfaces.

See [Security](security.md), [Threat Model](threat-model.md), and [Sync and Cloud](sync-and-cloud.md) for the implemented boundaries.
