# CLI Usage

This page documents the command surface in [`axiom-cli@7b436af`](https://github.com/axiom-vault/axiom-cli/commit/7b436aff5a8d5236d075a9e2bfe7f998d171b83c). A parsed command is not necessarily an operationally complete capability; statuses use the [site vocabulary](README.md#status-vocabulary). The CLI pins an older core revision, tracked for update in [CLI #25](https://github.com/axiom-vault/axiom-cli/issues/25).

## Local vault and file commands — **available**

```text
axiom vault create --name NAME --path PATH [--strength interactive|moderate|sensitive]
axiom vault open --path PATH
axiom vault info --path PATH
axiom vault check --path PATH [--shallow]

axiom file list --vault-path PATH [--dir /]
axiom file add --vault-path PATH --source FILE --dest /VAULT/PATH
axiom file extract --vault-path PATH --source /VAULT/PATH --dest FILE
axiom file mkdir --vault-path PATH --dir /VAULT/PATH
axiom file remove --vault-path PATH --file /VAULT/PATH
```

“Available” here means the command exists at the reviewed revision, not that the vault format is stable or the implementation is production hardened. Import/export currently buffer whole files and ordinary destination writes are not an atomic authenticated streaming boundary ([CLI #24](https://github.com/axiom-vault/axiom-cli/issues/24)).

## Password and recovery — **available** / migration **experimental-incomplete**

```text
axiom password change --path PATH
axiom password reset --path PATH
axiom recovery show-key --path PATH
axiom recovery enable --path PATH
axiom vault migrate --path PATH [--dry-run]
```

Normal password/recovery commands exist. Do not treat migration as an authenticated atomic format transition: the core FFI path accepts but does not consume its password, rollback is incomplete, and generated recovery-material ownership is unresolved ([core #17](https://github.com/axiom-vault/axiom-core/issues/17)). Back up and verify non-critical test vaults before migration.

## Google Drive — **experimental-incomplete**

```bash
axiom remote gdrive auth --output ~/gdrive-tokens.json
axiom remote gdrive create \
  --name CloudVault \
  --folder-id YOUR_FOLDER_ID \
  --tokens ~/gdrive-tokens.json
axiom remote gdrive open \
  --folder-id YOUR_FOLDER_ID \
  --tokens ~/gdrive-tokens.json
```

These are syntactically supported. The token-bearing provider configuration can become portable vault data, so the reviewed implementation does not guarantee local-only credentials. See [Sync and Cloud](sync-and-cloud.md#google-drive-credentials), [core #11](https://github.com/axiom-vault/axiom-core/issues/11), and [CLI #22](https://github.com/axiom-vault/axiom-cli/issues/22). iCloud and Dropbox commands are placeholders and **unavailable**.

## Sync — **experimental-incomplete** / background modes **scaffolded**

```bash
axiom sync run --vault-path ~/my-vault --strategy keep-both
axiom sync status --vault-path ~/my-vault
axiom sync conflicts --vault-path ~/my-vault
axiom sync resolve \
  --vault-path ~/my-vault \
  --file /path/in/vault \
  --strategy prefer-local
axiom sync configure \
  --vault-path ~/my-vault \
  --mode periodic \
  --interval 300
```

Accepted strategies are `keep-both`, `prefer-local`, and `prefer-remote`; accepted modes are `manual`, `on-demand`, `periodic`, and `hybrid`. Remote downloads are not durably persisted, and configuring a mode does not turn the CLI into a verified background service. See [core #15](https://github.com/axiom-vault/axiom-core/issues/15).

## Mounts

```bash
axiom mount webdav --path ~/my-vault --port 8080

# Only when built with the optional fuse feature:
axiom mount fuse --path ~/my-vault ~/my-vault-mount
```

- FUSE is **experimental-incomplete** and available only in builds with the feature/platform support.
- WebDAV is **experimental-incomplete** as an access layer and **unavailable** as an authenticated service. The CLI selects `127.0.0.1`, but the endpoint requires no request credentials and core does not enforce loopback for other callers ([core #12](https://github.com/axiom-vault/axiom-core/issues/12), [CLI #23](https://github.com/axiom-vault/axiom-cli/issues/23)). Do not expose it or use it with sensitive data.
