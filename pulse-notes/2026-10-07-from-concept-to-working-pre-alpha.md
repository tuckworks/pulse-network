# From concept to working pre-alpha

**October 7, 2026 | Retrospective**

Pulse development began on September 10, 2026, with an architecture for private messaging that would not require conventional accounts, permanent message servers, or a fixed network location for an identity.

The first month moved much of that work into running clients. It also required several changes to the original design. Some followed successful device tests. Others came from failures that exposed assumptions in the network or authorization model.

This note records the principal changes through October 7.

## Identity and device authority

The original identity model needed to support multiple devices without distributing the same private key to each one. That requirement affected device enrollment, revocation, and recovery.

The current direction uses a stable identity anchor with independently keyed devices and authenticated membership state. In the consumer model, a Primary Device administers sensitive changes. Authorized devices can continue ordinary communication without requiring the Primary to remain online.

Implementation work expanded from creating and storing a local identity to maintaining verifiable transitions in device authority. Removing a device also requires contacts to recognize the new state and exclude the removed endpoint from future protected communication.

This remains an active protocol area, particularly where devices have been disconnected for long periods.

## Conversation state and delivery

Early messaging work established a separate identity for the logical event in a conversation.

That decision became important when a delivery needed to be retried or carried over a different network. The same conversation event may have encrypted deliveries for separate authorized devices. Each attempt can use a different carrier while retaining the original event identity.

The recipient's acceptance of an event and the return of an authenticated receipt determine the Delivered state. A successful network write, relay handoff, or local queue operation provides a different kind of evidence.

This separation has been used throughout later relay, roaming, and cellular work. It also provides the message-level foundation for future store-and-forward transport.

## Linked devices and relationship ingress

By late September, linking a device had raised a problem beyond synchronizing conversation history.

An independently keyed device can be authorized under an existing identity without having a session with every contact of that identity. If the Primary Device is offline, the new device still needs a way to approach those existing relationships and establish its own authenticated communication.

The Relationship Ingress Capability work grew out of that case. A limited-purpose ingress value identifies an entry point for a relationship, while device authorization and session authentication remain separate checks.

On September 27, the bounded Primary-off test reached the intended result. An independently keyed linked device became eligible for an existing relationship and communicated while the Primary was unavailable. When the devices later reconnected, the conversation state converged without duplicating the logical event.

Subsequent revocation testing addressed the reverse transition. Once a contact had accepted authenticated removal state, the revoked device was rejected and the relationship used its updated ingress state.

The results were obtained in a defined LAN topology. General Internet enrollment, larger device sets, and propagation to disconnected contacts still required separate work.

## Relay, cellular, and introduction experiments

Network testing accelerated in early October.

On October 1, relay and roaming tests exercised an existing authenticated relationship over non-LAN connections. On October 3, a bounded Android LTE and native Mac experiment carried protected traffic in both directions. The devices had first exchanged introduction information through an existing permitted path.

The carrier was able to transport the conversation. The introduction still depended on information established elsewhere.

Removing that prior path exposed a separate networking problem. Two devices may have an authenticated contact relationship and valid encrypted sessions, yet lack a current network location through which to contact one another.

The October 7 experiments concentrated on that point. Initial TCP and remote QUIC lookup trials failed to provide a fresh introduction. Later trials succeeded with explicitly provisioned lookup-node locations, including reuse after the earlier data and introduction paths were retired.

Those experiments established a bounded lookup-to-carrier path and demonstrated that known participating nodes could be reused. They did not establish how unknown participating nodes would be found privately across changing networks.

Fresh peer introduction is therefore still a primary research problem. The design must account for discovery and reachability without making a permanent identity directory or hosted inbox a required dependency.

## Recovery boundaries

Recovery work also became more specific during implementation.

Starting a new identity cannot grant access to an older identity merely because some of its files remain on the same device. Historical data and current authorization have to be handled separately.

The current approach provides for a bounded recovery request, potentially with explicit assistance from a former contact who still holds legitimate conversation records. The contact must approve the request under the applicable continuity rules. A reachable recovery endpoint supplies a communication path only.

Several cases remain unresolved, including catastrophic loss where no authorized device or eligible copy of the needed history survives. Recovery cannot be assumed to reconstruct unavailable information.

## Project direction

The project continues under the line **Private communication with no permanent home.**

Its broader objective is **trusted communication for people who cannot assume the network will be there.** That includes unreliable Internet access, changing routes, unavailable devices, and the loss of optional infrastructure.

A communication opportunity must still exist at some point. Pulse cannot deliver through a permanent physical partition without a live connection, subsequent encounter, or suitable stored forwarding path.

## Status at the end of the first month

Pulse now has working pre-alpha clients and tested checkpoints for authenticated contact relationships, independent device authorization, protected message delivery, authenticated receipts, linked-device convergence, bounded Primary-off operation, device removal, and several local and non-LAN transport configurations.

The remaining work is substantial. General private discovery has not been established. Mobile background availability and energy behavior need sustained validation. Volunteer storage and multi-hop forwarding are incomplete. The production cryptographic suite remains open, as do groups, media, formal interoperability, release hardening, and independent security review.

Future Pulse Notes will record results that materially change these assessments or the underlying design.
