# Sync and Cloud

AxiomVault is designed to encrypt data before it touches cloud storage.

## Current remote support

- Google Drive with OAuth2 and resumable uploads
- Local filesystem storage for offline or self-hosted workflows

## Planned remote support

- iCloud
- Dropbox
- OneDrive

## Sync behavior

The sync engine supports:

- On-demand sync runs
- Periodic background sync
- ETag-based conflict detection
- Conflict resolution strategies such as `keep-both`, prefer local, prefer remote, and manual handling
- Retry with exponential backoff

## Typical flow

```bash
axiom remote gdrive auth --output ~/gdrive-tokens.json
axiom sync run --vault-path ~/my-vault --strategy keep-both
axiom sync status --vault-path ~/my-vault
```
