# MCP Status

## Current status
AxiomVault does **not** currently ship a documented **Model Context Protocol (MCP)** server, MCP client integration, or MCP-specific CLI workflow in this repository.

Today, the supported interface described by this mdBook is the regular command-line workflow in `axiom-cli`.

## What is supported today
- Local CLI-driven vault operations
- Shared Rust core libraries used by the CLI and optional access layers
- Documentation for native commands, sync, vault format, and security boundaries

## What is not supported today
The docs do **not** currently describe or promise:
- a first-party MCP server for exposing vault operations to external tools
- an MCP client for connecting AxiomVault to other MCP servers
- MCP-specific authentication, permission prompts, or sandbox policies
- a stable MCP API contract

## Planned or future work
MCP-based tooling may be explored later, but this repository does not currently document an implemented MCP feature set. Until code and release notes exist, treat MCP support as **not implemented**.

## Guidance for contributors and evaluators
If you need automation today, use the documented CLI directly and review the source before depending on behavior as an API contract.

## See also
- [Overview](README.md)
- [CLI Usage](cli.md)
- [Current Limitations](current-limitations.md)
