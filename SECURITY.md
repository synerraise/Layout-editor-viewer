# Security Policy

## Reporting a vulnerability

Do not disclose an unpatched vulnerability in a public issue. Use the private
security-reporting channel configured for the official distribution or contact
the supplier identified in the applicable customer agreement. Include the
affected version, platform, impact, reproduction steps, and a minimal test file
when safe and authorized.

Never include proprietary chip-layout or foundry data unless its owner has
approved disclosure. Encrypt sensitive attachments using the method agreed with
the support contact.

## Supported versions

Until a long-term-support channel is announced, security fixes target the most
recent released minor version. Customers should reproduce an issue on the
latest patch release where practical. Older versions may be investigated, but a
fix can require upgrading.

## Release security controls

Release candidates must pass the locked dependency audit and malformed-GDS
tests in `.github/workflows/security.yml`. Official releases include SHA-256
checksums, an SPDX JSON software bill of materials for each native executable,
and GitHub build-provenance attestations. Unsigned packages must continue to be
identified as unsigned until production signing identities are configured.

Layout AI Agent is not a sandbox. Treat GDS and native projects as untrusted
input, open them on appropriately protected systems, and retain independent
backups.

