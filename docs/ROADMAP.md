# Pulse Roadmap and Development Status

**October 7, 2026 | Pre-alpha**

Pulse development is organized around protocol requirements, implementation work, and physical tests on actual devices. The results below describe individual checkpoints. They are not a completed product acceptance test.

## Tested pre-alpha capabilities

The following have been exercised in bounded configurations:

- Local cryptographic identities and authenticated contact relationships.
- Linked devices with independent cryptographic keys.
- Durable conversation events and encrypted delivery to individual devices.
- Authenticated recipient receipts and duplicate-event handling.
- Linked-device conversation convergence.
- Messaging with the Primary Device offline in a defined test topology.
- Authenticated device removal and relationship fencing.
- Local-network messaging and carrier changes.
- Relay and network-roaming behavior.
- Protected carrier exchange over real cellular connections between previously authorized peers.

These tests used specific devices, network configurations, and setup conditions. Some Internet trials required an existing introduction route or explicitly supplied lookup-node addresses.

## Current development priorities

### Peer introduction and discovery

Develop a private way for authorized peers to find new reachable communication opportunities after previous routes have failed. Existing known-node lookup experiments provide a limited foundation. Unknown-node discovery and broad reachability remain open.

### Delayed delivery

Continue the design and implementation of bounded custody on participating peers, including authenticated deposits, retrieval, resource limits, redundancy, expiry, forwarding, and receipt return.

### Mobile networking

Measure and improve behavior during background execution, network changes, and platform suspension. Battery and thermal cost are part of acceptance, particularly for devices that may carry traffic for others.

### Device continuity and recovery

Extend tested authorization, revocation, and recovery behavior to additional loss, replacement, and disconnected-device scenarios.

### Production cryptography

Select and specify the production identity and session constructions. Hybrid post-quantum work remains subject to library selection, interoperability testing, and independent review.

## Further work

The broader roadmap includes:

- Routing and NAT traversal under the selected privacy policies.
- Multi-hop forwarding and resilient transient storage.
- Canonical protocol encodings and interoperability test vectors.
- Groups and group membership changes.
- Encrypted attachments, voice, video, and other media.
- Secure local storage on each supported platform.
- Capture protections and limits on plaintext retention.
- Signed and reproducible releases with authenticated updates.
- Desktop and mobile installation and distribution.
- Adversarial testing and independent security review.

## Release criteria

A production-security claim requires a finalized and documented protocol, validated security-sensitive state machines, a defined release and update process, sustained testing across supported platforms, independent cryptographic review, and an implementation security audit.

The findings and remaining limitations will need to be documented before production distribution.

## Source publication

The implementation remains private during this stage. Before publishing source, the project will review its contents and history, remove material that does not belong in the public repository, and select an appropriate license.
