# AxiomVault docs

Standalone mdBook documentation site for GitHub Pages.

## Why mdBook?

mdBook fits this repo well because it is Rust-native, fast, markdown-first, and simple to deploy with GitHub Pages.

## Local preview

Prerequisites:

- Rust toolchain
- `mdbook` (`cargo install mdbook`)

Run locally:

```bash
mdbook serve --open
```

## Build

```bash
mdbook build
```

The generated site is written to `book/`.

## Deploy to GitHub Pages

This repo includes `.github/workflows/pages.yml`.

In GitHub:

1. Push this repository.
2. Open **Settings → Pages**.
3. Set **Build and deployment → Source** to **GitHub Actions**.

For an org/user Pages repo named `axiom-vault.github.io`, the site will publish at:

- `https://axiom-vault.github.io/`
