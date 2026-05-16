# Troubleshooting

## `mdbook: command not found`

Install it with:

```bash
cargo install mdbook
```

## Mermaid diagrams render as code blocks

Install the Mermaid preprocessor and rebuild:

```bash
cargo install mdbook-mermaid
mdbook build
```

## GitHub Pages build fails

Check these first:
- GitHub Pages is configured to use **GitHub Actions**
- The workflow has permission to deploy pages
- `mdbook build` succeeds locally
- `mdbook-mermaid` is installed locally if Mermaid diagrams were added

## Broken CLI examples

The CLI is still evolving. If a command has drifted:
1. Check `axiom --help`
2. Compare against the latest `axiom-cli` README
3. Update the affected page and `src/SUMMARY.md` if needed

## Search or navigation issues

Rebuild the site locally:

```bash
mdbook build
mdbook serve --open
```
