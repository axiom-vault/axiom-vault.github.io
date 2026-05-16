# CLI Usage

The `axiom` binary is the main operator interface for local vaults, remotes, sync, and mounts.

## Vault commands

- `axiom vault create`
- `axiom vault open`
- `axiom vault info`
- `axiom vault check`
- `axiom vault migrate`

## File commands

- `axiom file list`
- `axiom file add`
- `axiom file extract`
- `axiom file mkdir`
- `axiom file remove`

## Password and recovery

- `axiom password change`
- `axiom password reset`
- `axiom recovery show-key`
- `axiom recovery enable`

## Remotes

### Google Drive

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

Treat the OAuth token file as a secret: keep it out of version control, restrict filesystem permissions, and prefer platform secret storage when the implementation supports it.

### Planned remotes

- iCloud
- Dropbox

## Sync

```bash
axiom sync run --vault-path ~/my-vault --strategy keep-both
axiom sync status --vault-path ~/my-vault
axiom sync configure --vault-path ~/my-vault --mode periodic --interval 300
```

## Mounts

- `axiom mount webdav`
- `axiom mount fuse`

## KDF strength levels

```text
--strength interactive
--strength moderate
--strength sensitive
```
