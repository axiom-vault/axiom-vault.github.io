# Current Limitations

AxiomVault is **not production ready**. This page uses the [site status vocabulary](README.md#status-vocabulary) for `axiom-core@b6520ff` and `axiom-cli@7b436af`. Open issues describe planned work, not shipped fixes.

## High-impact boundaries

| Boundary | Status | Consequence |
| --- | --- | --- |
| Multi-device convergence | **experimental-incomplete** | Remote downloads are not persisted before sync state can advance; do not use sync as backup/restore ([core #15](https://github.com/axiom-vault/axiom-core/issues/15)). |
| Background sync | **scaffolded** | Modes/configuration exist without a verified long-running CLI lifecycle. |
| Bounded-memory streaming | **unavailable** | Crypto and higher layers buffer complete data; large files can use memory proportional to size ([core #18](https://github.com/axiom-vault/axiom-core/issues/18), [CLI #24](https://github.com/axiom-vault/axiom-cli/issues/24)). |
| Authenticated WebDAV | **unavailable** | The CLI endpoint is loopback-bound but unauthenticated; reusable core binding is not restricted to loopback ([core #12](https://github.com/axiom-vault/axiom-core/issues/12), [CLI #23](https://github.com/axiom-vault/axiom-cli/issues/23)). |
| Local-only OAuth credentials | **unavailable** | Token-bearing provider config can be uploaded; affected credentials should be revoked/rotated ([core #11](https://github.com/axiom-vault/axiom-core/issues/11), [CLI #22](https://github.com/axiom-vault/axiom-cli/issues/22)). |
| Snapshot rollback detection / TOFU | **unavailable** | Authentication does not establish freshness and no trusted anchor exists ([core #13](https://github.com/axiom-vault/axiom-core/issues/13)). |
| Authenticated atomic migration | **experimental-incomplete** | Legacy FFI migration ignores its password and lacks complete rollback/recovery-output semantics ([core #17](https://github.com/axiom-vault/axiom-core/issues/17)). |
| Plaintext local-index protection | **experimental-incomplete** | Optional SQLite metadata cache is not encrypted and its permission/wipe path does not consistently fail closed ([core #16](https://github.com/axiom-vault/axiom-core/issues/16)). |

## Additional limitations

- No external security audit, formal verification, or stable-format guarantee is claimed.
- Vault mutations are not yet transactional across storage and the in-memory tree ([core #14](https://github.com/axiom-vault/axiom-core/issues/14)).
- Endpoint compromise remains decisive while a vault is unlocked.
- FUSE and WebDAV expose plaintext views and expand the attack surface.
- iCloud, Dropbox, and OneDrive CLI workflows are **unavailable**.
- Packaging, platform behavior, observability, and recovery edge cases remain immature.
- The CLI pins an older core revision; fixes on core `main` do not reach CLI users automatically ([CLI #25](https://github.com/axiom-vault/axiom-cli/issues/25)).

## Credential response for existing cloud vaults

If an affected revision created or opened a cloud vault, assume OAuth credentials may survive in provider history or backups. Revoke the grant, rotate client secrets where applicable, and re-authenticate only after both core and CLI credential-locality changes ship in the exact revision you run. Rewriting the newest config object is not sufficient to erase remote history.

## Recommended use today

Use AxiomVault for source review, contributor onboarding, and controlled experiments with disposable, non-critical data. Keep independent backups outside AxiomVault. Do not expose WebDAV, depend on cloud convergence, or infer freshness from successful decryption.
