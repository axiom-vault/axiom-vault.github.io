# Quickstart

## 1. Install the CLI

```bash
curl -fsSL https://raw.githubusercontent.com/axiom-vault/axiom-cli/main/install.sh | bash
```

Prefer a packaged release when available. If you use the install script, review it before execution and avoid running it on systems you do not trust with local credentials.

Other install paths include GitHub Releases, Homebrew, and building from source.

## 2. Create a vault

```bash
axiom vault create --name MyVault --path ~/my-vault
```

## 3. Add a file

```bash
axiom file add \
  --vault-path ~/my-vault \
  --source ~/secret.pdf \
  --dest /secret.pdf
```

## 4. Inspect contents

```bash
axiom file list --vault-path ~/my-vault
```

## 5. Extract a file

```bash
axiom file extract \
  --vault-path ~/my-vault \
  --source /secret.pdf \
  --dest ~/secret.pdf
```

## 6. Open an interactive session

```bash
axiom vault open --path ~/my-vault
```

## Optional: enable sync

```bash
axiom sync run --vault-path ~/my-vault --strategy keep-both
axiom sync status --vault-path ~/my-vault
```

## Optional: mount the vault

```bash
mkdir -p ~/my-vault-mount
axiom mount fuse --path ~/my-vault ~/my-vault-mount
```

## Build from source

```bash
git clone https://github.com/axiom-vault/axiom-cli.git
cd axiom-cli
cargo build --release
```
