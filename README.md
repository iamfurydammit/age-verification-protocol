### Age Verification Protocol (AVP)
### Overview

The Age Verification Protocol (AVP) is a privacy-preserving, decentralized protocol that enables access to age-restricted content by answering exactly one question:

Is the user an adult?

AVP is designed to protect minors without identifying users, without tracking behavior, and without creating records of access, in a manner consistent with the Constitution of the United States.

The protocol does not provide identity, reputation, accounts, profiles, or surveillance. It exists solely to prove non-minor status.

## Design Goals

AVP is built around the following non-negotiable goals:

### Single-question scope

The protocol answers only: “Is the holder an adult?”
No other attributes are exposed or inferable.

### One-time verification

Age is verified once using government-issued identification and a one-time proof-of-life (liveness) check.
No recurring verification is required.

### No identity disclosure

No names, addresses, document numbers, or identifiers are revealed to content sites or verifiers.

### No tracking or observation

It is cryptographically impossible to determine:

whether a token has been used

how many times it has been used

where it has been used

when it has been used

### No central database

Sensitive verification material is decentralized and cryptographically fragmented across independent hubs.

### Stateless verification

Proof verification produces no side effects, logs, counters, callbacks, or observable signals.

## Time-Based Eligibility Resolution

Adult eligibility is resolved through a time-based cryptographic commitment created at issuance.

The Adult Proof Token contains no date of birth, no age value, no counters, no timestamps, and no update mechanisms.
Eligibility emerges solely from the passage of time and local proof generation, without re-verification, renewal, refresh, smart contracts, or network interaction.

The token is passive, non-expiring, and matures naturally with the holder.
No authority, service, or platform participates in or observes this transition.

## Constitutionally Narrow

The protocol is narrowly tailored to protect minors while preserving anonymous access to lawful adult speech.

## Session Continuity & Token Loss

Age eligibility tokens are session-bound and may be invalidated at any time due to session termination, device disconnection, or loss of session continuity.

Loss of a token does not revoke age status.

Users may re-authenticate at any time to obtain a new token. Re-authentication may require out-of-band confirmation (e.g., email, SMS, or hardware confirmation).

AVP does not provide continuous identity verification, monitoring, or surveillance.
Session invalidation is a safety control, not a tracking mechanism.

## Client Activation & Session Entry

The AVP client remains inactive during normal device use and general web browsing.
Age-restricted content is inaccessible by default.

Age verification is performed only when a user explicitly initiates an adult session to access age-restricted content.

Initial session entry may require email-based confirmation in combination with a second confirmation method, such as:

SMS confirmation, or

Hardware-based confirmation

After session entry, email is not used for ongoing presence checks.
Continued access is governed solely by local session continuity and presence confirmation.

No age checks, presence checks, timers, or prompts occur prior to an explicit request for age-restricted content.

## What AVP Is Not

AVP explicitly does not attempt to solve:

Digital identity

KYC-as-a-service

User accounts or profiles

Reputation or trust scoring

Behavioral monitoring

Internet-wide filtering

Content moderation

Law enforcement access

Analytics or telemetry

Any system that introduces these properties is out of scope by design.

## High-Level Architecture
One-Time Age Verification (Issuance)

The user submits government-issued ID and completes a one-time proof-of-life scan.

The verification process checks age only.

Date of birth is used once to create a cryptographic commitment.

Raw personal data is not stored or recoverable.

Verification artifacts are cryptographically fragmented across independent hubs.

A non-transferable Adult Proof Token (APT) is issued to the user.

This is the only moment at which personal data is processed.

## Local Credential Control

The Adult Proof Token is delivered to the user and stored locally.

A local software login may be used only to unlock the token.

Email and SMS are permitted only for session entry and recovery.

No network interaction occurs during normal browsing.

Accessing Age-Restricted Content

Age-restricted content self-declares its restriction.

When such content is requested:

The client generates a local, zero-knowledge proof.

The proof answers only: “Is the holder an adult?”

Verification is:

Stateless

Anonymous

Offline-capable

✔ Valid proof → content is delivered
✖ Invalid or absent proof → content is never transmitted

Users never see denied content.
No records of access are created.

## Token Characteristics

Non-transferable

Stored locally

Not an account, wallet, or profile

Cannot be queried, refreshed, updated, revoked, or counted

Generates local, stateless, zero-knowledge proofs

Reveals only: adult / not adult

Not enumerable

It is cryptographically impossible to count, estimate, or infer the number of issued tokens, active sessions, or participating users.

## Age-Domain Isolation (Mandatory)

Adult Proof Tokens and child-domain credentials exist in mutually exclusive interaction domains.

It is cryptographically and structurally impossible for:

an adult token to interact with a child token

a child token to interact with an adult token

This applies to web browsing, social platforms, messaging systems, discovery, visibility, and interaction.

Adult users cannot see that child users exist, and vice versa.

There is no messaging, discovery, shared spaces, or cross-domain signaling.

Adult and child domains share no cryptographic namespace.

There is no shared key space, proof system, identifier format, circuit, domain separator, or trust root.
Cross-domain proofs are not merely rejected — they are structurally invalid and non-representable.

This separation is enforced by protocol design, not moderation or policy.

## Explicit Non-Goals

AVP explicitly does not:

Track age progression

Issue expiring credentials

Require periodic renewal or re-verification

Perform background checks or scheduled updates

All eligibility resolution occurs locally and deterministically, without storage, logging, or external coordination.

Security and Privacy Properties

AVP guarantees:

No post-issuance observation

No usage counting

No correlation across sites

No reconstruction of age or identity

No centralized breach risk

No issuer visibility into usage

These properties are enforced by architecture, not by policy.

## Constitutional Considerations

AVP is designed to:

Preserve anonymous access to lawful adult speech

Avoid chilling effects on expression

Use the least restrictive means to protect minors

Avoid identity-based access controls

Avoid logging or monitoring of viewing behavior

Age checks occur only at the point of requesting age-restricted content and reveal no identity information.

## Repository Structure

This repository contains:

A language-agnostic protocol specification

Formal invariants and threat modeling

Legal and constitutional design rationale

A Rust reference implementation demonstrating protocol invariants

The protocol itself is implementation-independent.

## Status

This project is currently in the specification and reference implementation phase.

Protocol invariants are considered foundational and must not be altered without a major version change.

## License

This repository is published for public review, discussion, and implementation.

Licensing details are specified in the repository root.
