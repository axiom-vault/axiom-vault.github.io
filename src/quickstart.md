# Quickstart

This quickstart exercises **available** local commands from [`axiom-cli@7b436af`](https://github.com/axiom-vault/axiom-cli/commit/7b436aff5a8d5236d075a9e2bfe7f998d171b83c). Use non-critical test data: AxiomVault is not production ready.

## 1. Install the CLI

```bash
curl -fsSL https://raw.githubusercontent.com/axiom-vault/axiom-cli/main/install.sh | bash
```

Alternatively, build the reviewed source revision:

```bash
git clone https://github.com/axiom-vault/axiom-cli.git
cd axiom-cli
git checkout 7b436aff5a8d5236d075a9e2bfe7f998d171b83c
cargo build --release
```

## 2. Create a vault

```bash
axiom vault create --name MyVault --path ~/my-vault
```

Store the displayed recovery mnemonic separately and securely.

## 3. Add and inspect a test file

```bash
printf 'non-critical test data\n' > ~/axiom-test.txt
axiom file add \
  --vault-path ~/my-vault \
  --source ~/axiom-test.txt \
  --dest /axiom-test.txt
axiom file list --vault-path ~/my-vault
```

## 4. Extract it

Choose a destination that does not already contain important data:

```bash
axiom file extract \
  --vault-path ~/my-vault \
  --source /axiom-test.txt \
  --dest ~/axiom-test-restored.txt
```

Current import/export paths buffer complete files, and safe atomic plaintext publication remains incomplete ([CLI #24](https://github.com/axiom-vault/axiom-cli/issues/24)).

## 5. Open and inspect the vault

```bash
axiom vault open --path ~/my-vault
axiom vault info --path ~/my-vault
axiom vault check --path ~/my-vault
```

## Do not treat sync as a backup yet

`axiom sync run` is **experimental-incomplete**: downloaded remote bytes are not durably applied, so multi-device convergence is not established ([core #15](https://github.com/axiom-vault/axiom-core/issues/15)). Google Drive credentials can also enter portable configuration ([core #11](https://github.com/axiom-vault/axiom-core/issues/11), [CLI #22](https://github.com/axiom-vault/axiom-cli/issues/22)). See [Sync and Cloud](sync-and-cloud.md) before testing cloud commands.

## Avoid WebDAV for sensitive data

The WebDAV command exists, but request authentication is **unavailable** at the reviewed revisions. CLI loopback binding does not protect against untrusted local processes. See [CLI Usage](cli.md#mounts).
