# Security

## Important warning

AxiomVault is still in **early development** and is **not production ready**.

## Security model

- Client-side encryption only
- Zero-knowledge architecture
- Authenticated encryption on every chunk
- Chunk ordering protection
- Memory zeroization for key material
- Constant-time comparisons where appropriate
- No plaintext secrets in logs

## Crypto and data protection

| Area | Detail |
| --- | --- |
| Content encryption | XChaCha20-Poly1305 |
| Key derivation | Argon2id |
| Hashing | Blake2b |
| Recovery key | 24-word BIP39 mnemonic |

## Trust assumptions

AxiomVault's security depends on these assumptions:

- Build artifacts are produced from reviewed source.
- Rust's memory safety guarantees hold outside explicitly-audited `unsafe` blocks.
- The underlying cryptographic primitives remain sound.
- The OS kernel and FUSE subsystem correctly enforce mount permissions.

## Key hierarchy

```text
User password
  |
  v
Argon2id(password, salt) --> Password KEK --> wraps Master Key
                                             | derives file/dir keys (Blake2b)

Recovery key (24 BIP39 words, shown once)
  |
  v
Blake2b(entropy, context) --> Recovery KEK --> wraps same Master Key
```

The master key is randomly generated and stored only in wrapped form. Two independent KEKs can unwrap it: one from the password and one from the recovery mnemonic.

## File encryption

Files are encrypted using chunked streaming encryption. Each chunk is independently authenticated, and chunk indices are included in authenticated data to prevent reordering or truncation.

## Security practices

- Dependency auditing with `cargo audit`
- Secret scanning with `gitleaks`
- Lint enforcement with `cargo clippy -D warnings`
- `// SAFETY:` comments for every `unsafe` block
- `Zeroize` and `ZeroizeOnDrop` on sensitive key material
- Constant-time comparisons for sensitive equality checks

## Supported versions

Only the latest release receives security patches.
