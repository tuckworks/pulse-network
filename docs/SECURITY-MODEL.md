# Pulse Security Model

**Public threat-model overview | October 7, 2026 | Pre-alpha**

This document records the principal threats considered during Pulse development. It describes security requirements and expected failure behavior. The implementation and protocol have not been independently audited.

## Security assumptions

Pulse treats network infrastructure as untrusted. An adversary may operate a relay or storage peer, monitor connections, interfere with traffic, or prevent messages from arriving.

Authenticated identity and device state determine who is eligible to communicate. Possession of a network address, relay connection, or stored ciphertext provides no additional authority.

When authentication or encryption fails, the message remains queued. The client must not send it using plaintext or an unauthenticated fallback.

## Threats considered

### Network and relay operators

A relay may inspect available routing metadata, copy protected traffic, delay delivery, reorder packets, or drop messages. It should not obtain message plaintext or be able to forge authenticated conversation events through its role as a carrier.

A malicious operator can still disrupt availability, and some metadata remains observable.

### Transient-storage peers

A future volunteer storage peer may have complete control of the machine holding encrypted message material. Stored objects could be inspected, copied, or retained after the intended period.

The storage design requires protected content to remain opaque. Deposit and retrieval authority must be independently verified. Possession of an encrypted object must not confer message-decryption keys or relationship membership.

The live custody protocol remains under development.

### Active interception

An attacker may try to substitute identities or session material during connection establishment, replay older messages, or force a weaker communication mode.

Pulse requires authenticated identity continuity, verification of device authority, and rejection of invalid or stale protocol state. Production cryptographic constructions and their test vectors are not yet finalized.

### Stolen or compromised devices

A locked stolen device presents a local storage and key-protection problem. Security depends in part on platform facilities and their correct use.

An attacker controlling an unlocked endpoint has a substantially stronger position. They may see plaintext and acquire current secrets. Forward secrecy and recovery after compromise are design requirements, but the guarantees depend on the final protocol and the extent of the compromise.

### Revoked devices

A removed device may retain messages and keys from its authorized period. Future relationship state must exclude it once valid revocation and any required rekeying have been accepted.

An offline contact may temporarily hold an older authorization view. Revocation cannot be instantaneous across a network partition.

### Traffic analysis

Observers may correlate network addresses, packet timing, volumes, and repeated traffic patterns. Pulse is intended to reduce avoidable metadata exposure, including through relationship-scoped identifiers and replaceable routing paths.

It does not claim anonymity against a global passive observer.

### Future cryptanalytic attacks

Recorded ciphertext may be subject to later attacks against the algorithms used to protect it. Pulse is evaluating hybrid classical and post-quantum approaches, but the production identity and session suite has not been selected.

## Endpoint and physical limits

An intended recipient can disclose a message. An external camera can capture a screen. A fully compromised unlocked device may expose all plaintext it can access.

Physical coercion and destruction of every remaining authorized copy of data fall outside the confidentiality and recovery properties a messaging protocol can provide.

## Confidentiality and availability

Pulse may be unable to deliver a message when no authenticated route exists. That failure must remain visible to the sender.

Loss of network availability does not justify relaxing encryption, identity verification, or device-authorization requirements. An acknowledgement from a relay or storage peer must also remain distinct from an authenticated recipient receipt.

## Current limitations

The following remain unproven or unfinished:

- General private Internet discovery and reliable reachability through arbitrary NAT arrangements.
- Production mobile background availability and measured resource consumption.
- Complete decentralized storage, forwarding, and recovery of delayed messages.
- Final production cryptography and reviewed protocol encodings.
- Device recovery and revocation across broader failure scenarios.
- Independent cryptographic review and implementation security audit.

Public security claims will be revised as the protocol and supporting evidence mature.
