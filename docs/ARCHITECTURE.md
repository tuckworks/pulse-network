# Pulse Architecture

**Public technical overview | October 7, 2026 | Pre-alpha**

Pulse is being developed as a secure-messaging protocol and reference client. This document describes the current architectural direction. The detailed protocol, including several cryptographic and networking constructions, remains under development.

## Identity and device authorization

A Pulse identity is created locally. Its stable cryptographic identity is independent of the device's current network address.

An identity may have several authorized devices. Each device has separate key material, and its authority is represented in authenticated device state. The consumer model includes a Primary Device responsible for sensitive administration. Ordinary messaging between authorized devices and contacts does not require that Primary to remain online.

The design avoids distributing a single master private key to every device. Membership changes, key changes, and revocation must be verified against authenticated identity state.

## Contact relationships

A contact relationship records trust between identities. Network reachability is handled separately.

A device joining an existing identity may need to communicate with a contact it has never reached directly. This becomes difficult when the Primary Device is unavailable and the new device cannot use another device's session keys.

Pulse's relationship-ingress work addresses that case. A limited-purpose, rotating ingress value can help an eligible device find an existing relationship. The contact must still authenticate the device and verify its authorization. Ingress information carries no independent right to join a conversation.

## Messages and transport

Pulse keeps three kinds of state separate:

1. **Conversation event:** a durable logical message or conversation-state change.
2. **Device delivery:** protected material addressed to a specific authorized device and session.
3. **Carrier:** the network connection used to move that material.

A conversation event retains its identity through retries. When a carrier closes or changes, the sender can attempt another eligible path using the existing event. Recipient-side acceptance and deduplication operate on the protected event, rather than treating each network attempt as a new message.

Local connections, Internet relays, and temporary cellular carriers have been exercised using this approach. Store-and-forward transport is part of the longer-term design.

## Delivery acknowledgements

Pulse distinguishes carrier acceptance from recipient delivery.

A socket write or relay acknowledgement can confirm progress along a route. The user-visible Delivered state requires durable acceptance by the intended endpoint and the return of an authenticated receipt for the corresponding protected event.

A missing receipt leaves the sender without conclusive evidence of delivery, even when some network activity succeeded.

## Device revocation

Device removal is represented by authenticated state changes. Once a contact accepts the updated state, the revoked device must be excluded from future eligible communication and the affected relationship must advance its protected state as required.

There are unavoidable delays when devices are offline. A contact cannot enforce a revocation it has not received. The project does not assume immediate synchronization across disconnected participants.

## Recovery

Recovery depends on which authorized devices and conversation records remain available.

An ordinary contact invitation cannot restore an existing identity or authorize access to its private history. Recovery of conversation data may involve an already-authorized device or explicit approval from a contact retaining the relevant records.

The path used to submit a recovery request does not supply the authority required to approve it.

## Intermittent delivery and peer storage

The planned network allows encrypted messages to remain in temporary custody while the recipient is unavailable. Participating peers may hold or forward ciphertext under bounded storage and retention policies.

Storage and retrieval permissions must be separated. A peer storing a protected message should not receive its decryption keys or gain authority over the relationship.

This work is incomplete. Resource accounting, redundancy, secure custody, retrieval, acknowledgement return, and delivery across multiple intermittent hops remain active research areas.

## Internet reachability

Current experiments establish an important boundary in the network design.

Protected carriers have worked across non-LAN paths when participating devices already had suitable introduction information. Known-node lookup experiments have also shown that an existing protected introduction sequence can be used and reused under bounded conditions.

The outstanding issue is obtaining fresh reachable introductions without requiring a permanent directory of identity locations or one mandatory hosted service. The project has not demonstrated general private peer discovery or universal NAT traversal.

## Scope of current evidence

Pre-alpha tests have exercised authenticated relationships, independent device authorization, exact-device encrypted messaging, receipts, linked-device convergence, Primary-off operation, revocation, relays, roaming, and cellular carriers.

The network still needs broader reachability, mobile background and energy validation, peer custody and forwarding, final cryptographic constructions, interoperability, and external security review. Communication also requires some eventual path between participants; no protocol can deliver across a partition that remains permanently unbridged.
