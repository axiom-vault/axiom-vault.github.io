# YubiKey and Hardware-Key Status

## Current status
AxiomVault does **not** currently document or claim implemented support for **YubiKey**, **PIV/smartcard**, **FIDO2/WebAuthn**, or other hardware-backed key workflows in this repository.

The current documented recovery and unlock model is:
- password-derived key encryption
- recovery mnemonic wrapping the same master key

## What is supported today
- Password-based vault unlock
- Recovery via the documented mnemonic flow
- Software-based local key handling described in the current security pages

## What is not supported today
The docs do **not** currently promise:
- YubiKey-backed vault unlock
- hardware-enforced key wrapping or unwrapping
- smartcard or PIV integration
- FIDO2/WebAuthn login or recovery flows
- resident-key, touch-policy, or PIN-policy integration

## Security implications
Because hardware-backed key workflows are not currently documented as implemented, users should assume vault access depends on the host device, password handling, recovery phrase protection, and local operational security.

Hardware keys may become useful in the future for stronger local key protection or operator workflows, but that is **not a current feature claim**.

## Guidance for contributors and evaluators
Avoid presenting AxiomVault as if it already has phishing-resistant or hardware-backed unlock guarantees. If hardware-key support is added later, the docs should describe the exact mechanism, platform coverage, failure modes, and recovery implications.

## See also
- [Security](security.md)
- [Threat Model](threat-model.md)
- [Current Limitations](current-limitations.md)
