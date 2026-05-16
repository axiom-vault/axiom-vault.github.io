# Contributors

## Workspace layout

- `axiom-cli/` — CLI repository
- `axiom-core/` — core Rust workspace
- `axiom-vault.github.io/` — standalone docs site

## Local docs workflow

```bash
cd axiom-vault.github.io
cargo install mdbook mdbook-mermaid
mdbook serve --open
```

## Writing guidelines

- Keep pages markdown-first and easy to scan
- Prefer examples that match current CLI behavior
- Call out early-development caveats clearly
- Update `src/SUMMARY.md` when adding chapters

## Validation

```bash
mdbook build
```
