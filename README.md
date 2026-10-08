# Pulse

**Private communication with no permanent home.**

Pulse is an experimental secure-messaging network and reference client. It uses locally created cryptographic identities, independently authorized devices, and end-to-end encrypted conversations. Its network design allows communication over different available connections without requiring a permanent Pulse-operated message server.

The project began on September 10, 2026. It is currently in pre-alpha development.

> **Security status:** The protocol is unfinished and has not been independently audited. Pulse should not be used for high-risk communication.

## Design

Several requirements have remained consistent since the initial architecture work:

- Identity is created locally. A Pulse account, phone number, or email address is not required.
- Identity and network location are separate. A change of address or connection should not require a new identity.
- Each linked device has its own cryptographic keys and authorization. Devices do not share one copied master private key.
- End-to-end encryption is mandatory. Messages remain queued when a secure path is unavailable.
- Relays and other transport participants carry protected data. They have no authority to change contact relationships, device membership, or message contents.
- Offline delivery is intended to use temporary encrypted storage on participating peers, with limits on retention and resource use.
- The same conversation should work across local connections, Internet paths, relays, and future store-and-forward transports.

The longer-term objective is **trusted communication for people who cannot assume the network will be there.**

## Development status

The current clients have been used to test authenticated contacts, linked devices, encrypted messaging, device removal, and conversation synchronization. The testing includes configurations where the Primary Device is offline.

The networking work has also progressed beyond local connections. Relay and roaming tests have been completed, along with protected carrier exchanges over real cellular networks. Message identity and authenticated delivery receipts are preserved when a carrier changes.

These results apply to the specific pre-alpha configurations tested. They do not establish general Internet reachability or sustained reliability across devices and networks.

**Fresh peer introduction remains a major unresolved problem.** Existing contacts can establish protected communication when they have a usable introduction path. Finding a new reachable path after the previous one is lost still requires further work. Recent tests have used explicitly known lookup participants; general private discovery has not been demonstrated.

## Work ahead

Current research and development priorities include:

- Private discovery and reachability across changing Internet connections.
- Mobile background operation, battery use, and thermal limits.
- Peer storage, delayed delivery, and forwarding across multiple hops.
- Device continuity and recovery under more failure conditions.
- Final cryptographic suite selection, including hybrid post-quantum work.
- Groups, attachments, and media.
- Release security, interoperability, and independent review.

There is no production release.

## Repository contents

This repository contains Pulse's public project documentation and research history. Implementation work remains in a separate private repository while the protocol and publication requirements are reviewed.

- [Architecture](docs/ARCHITECTURE.md)
- [Security model](docs/SECURITY-MODEL.md)
- [Roadmap and development status](docs/ROADMAP.md)
- [Security policy](SECURITY.md)

## Pulse Notes

[Pulse Notes](pulse-notes/README.md) document major changes in the design, including experiments that altered earlier assumptions. The notes are published by milestone rather than by commit.

The first entry covers the initial month:

[October 7, 2026: From concept to working pre-alpha](pulse-notes/2026-10-07-from-concept-to-working-pre-alpha.md)

## License

The implementation has not been published, and an open-source license has not yet been selected. Licensing will be addressed before source publication.
