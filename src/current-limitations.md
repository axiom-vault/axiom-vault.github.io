# Current Limitations

## Read this first
AxiomVault is **not production ready**. The project is still shaping its format, sync behavior, and operational model.

## Product maturity limitations
- Early-development codebase with evolving architecture
- Documentation describes direction and current behavior, not a finished product contract
- Vault format details may change before a stable compatibility promise exists
- Security posture should be treated as promising but incomplete

## Security and assurance limitations
- No claim of external security audit in these docs
- No claim of formal verification or hardened release process
- Endpoint compromise is still a major risk when a vault is unlocked
- Optional access layers such as FUSE or WebDAV expand the exposed surface area
- No current claim of YubiKey, smartcard, FIDO2, or other hardware-backed key protection

## Platform and backend limitations
- Current remote support is limited to Google Drive and local filesystem workflows
- Planned providers such as iCloud, Dropbox, and OneDrive are not yet current capabilities
- No current MCP server or MCP client workflow is documented as a supported interface
- Cross-platform behavior may still vary as the CLI and shared core mature

## Operational limitations
- Recovery, conflict handling, and sync edge cases need continued testing
- Background sync behavior depends on the surrounding client environment
- OAuth token handling and local secret storage should be reviewed carefully before broader deployment
- Observability, packaging, and installer polish are still incomplete

## Documentation limitations
- Some pages describe intended design boundaries rather than battle-tested guarantees
- Diagrams are simplified and do not replace code-level review
- Newly added status pages for MCP and hardware keys are intentionally conservative and should not be read as feature promises
- These docs should help contributors and evaluators, not serve as a certification of readiness

## Recommended use today
A reasonable current use case is:
- internal development
- architecture review
- contributor onboarding
- controlled experimentation with non-critical data

Avoid presenting AxiomVault as a finished consumer security product until the project has stable releases, stronger compatibility guarantees, and broader verification.
