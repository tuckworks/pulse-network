# Security Policy

**Current status: Pre-alpha**

Pulse is undergoing protocol and implementation development. Its cryptography, network behavior, and device-security model have not received an independent security audit.

Current builds are intended for development and testing. They should not be relied upon for sensitive or safety-critical communication.

## Reporting vulnerabilities

Do not post exploitable findings, private keys, or other sensitive report material in a public GitHub issue.

Use GitHub's private vulnerability reporting feature if it is enabled for this repository. Otherwise, contact the repository maintainer privately before sending technical details.

A dedicated disclosure process is planned before a production release.

## Security requirements

The project requires:

- End-to-end encryption without a plaintext fallback.
- Established cryptographic primitives and appropriate reviewed libraries.
- Independent key material for authorized devices.
- Authentication of contacts, device changes, and protected message deliveries.
- No reliance on a relay or storage participant for message confidentiality.
- Encrypted local storage and careful handling of plaintext and secrets.
- Cryptographic agility and explicit versioning of security-sensitive protocol changes.
- Signed releases, controlled updates, and reproducible-build work before production distribution.

These requirements are being implemented and tested in stages. They should not be interpreted as completed security assurances.

## Known limits

A compromised, unlocked device can expose messages and cryptographic material available to it. Intended recipients can disclose conversation contents. An external camera can capture a screen. Network metadata may permit traffic analysis, including correlation of participants or activity.

Revocation information cannot take effect on a disconnected device before it reaches that device. Message history may also be unrecoverable if every authorized copy has been lost.

The [security model](docs/SECURITY-MODEL.md) describes the threat assumptions and outstanding work. Successful tests and field experiments do not replace external cryptographic review.
