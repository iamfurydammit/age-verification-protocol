**Age Verification Protocol (AVP)**

## Overview

The **Age Verification Protocol (AVP)** is a privacy-preserving, decentralized protocol that enables access to age-restricted content by answering **exactly one question**:

**Is the user an adult?**

AVP is designed to protect minors **without identifying users**, **without tracking behavior**, and **without creating records of access**, in a manner consistent with the Constitution of the United States.

The protocol does **not** provide identity, reputation, accounts, profiles, or surveillance. It exists solely to prove **non-minor status**.

## Design Goals

AVP is built around the following **non-negotiable goals**:

### Single-question scope
The protocol answers only: *“Is the holder an adult?”*
No other attributes are exposed or inferable.

### One-time verification
Age is verified once using government-issued identification and a liveness check.
No recurring verification is required.

### No identity disclosure
No names, addresses, document numbers, or identifiers are revealed to content sites.

### No tracking or observation
It is cryptographically impossible to determine:
* whether a token has been used
* how many times it has been used
* where it has been used
* when it has been used

### No central database
Sensitive verification material is decentralized and cryptographically fragmented across independent hubs.

### Stateless verification
Proof verification produces **no side effects**, logs, counters, or callbacks.

### Constitutionally narrow
The protocol is narrowly tailored to protect minors while preserving anonymous access to lawful adult speech.

## Session Continuity & Token Loss
Age eligibility tokens are **session-bound** and may be invalidated at any time due to session termination, device disconnection, or loss of session continuity.

Loss of a token **does not revoke age status**.

Users may re-authenticate at any time to obtain a new token.
Re-authentication may require **out-of-band confirmation** (e.g., email and SMS).

AVP does **not** provide continuous identity verification, monitoring, or surveillance.
Session invalidation is a **safety control**, not a tracking mechanism.

### Client Activation Boundary

The AVP client remains inactive during normal device use and browser operation.
Age verification and presence confirmation are triggered **only** when a web browser attempts to access age-restricted content.

No age checks, presence checks, timers, or prompts occur prior to such a request.

## What AVP Is Not
AVP explicitly does **not** attempt to solve:
* Digital identity
* KYC-as-a-service
* User accounts or profiles
* Reputation or trust scoring
* Behavioral monitoring
* Internet-wide filtering
* Content moderation
* Law enforcement access
* Analytics or telemetry

Any system that introduces these properties is **out of scope by design**.

## High-Level Architecture
### One-Time Age Verification (Issuance)

* The user submits government-issued ID and completes a one-time proof-of-life (liveness) scan.
* The verification process checks **age only**.
* Date of birth is used once to create a cryptographic commitment.
* Raw personal data is not stored or recoverable.
* Verification artifacts are cryptographically fragmented and distributed across independent hubs.
* A non-transferable **Adult Proof Token (APT)** is issued to the user.

This is the **only moment** at which personal data is processed.

### Local Credential Control

* The Adult Proof Token is delivered to the user and stored locally.
* A local software login may be used only to unlock the token (e.g., device security or biometrics).
* Email and SMS are permitted **only** for initial delivery and recovery.
* No network interaction occurs during normal browsing.

### Accessing Age-Restricted Content

* Age-restricted content self-declares its restriction.
* When such content is requested:

* The client generates a local, zero-knowledge proof.
* The proof answers only: *“Is the holder an adult?”*

Verification is:

* Stateless
* Anonymous
* Offline-capable

✔ Valid proof → content is delivered
✖ Invalid or absent proof → content is never transmitted

Users never see denied content.
No records of access are created.

## Date of Birth Handling

* Date of birth is never stored after issuance.
* A cryptographic commitment derived from DOB enables future age checks.
* Adulthood eligibility updates automatically as a function of time.
* No refresh, renewal, or re-verification is required.

## Security and Privacy Properties

AVP guarantees:

* No post-issuance observation
* No usage counting
* No correlation across sites
* No reconstruction of age or identity
* No centralized breach risk
* No issuer visibility into usage

These properties are enforced by **architecture**, not by policy.

## Constitutional Considerations

AVP is designed to:

* Preserve anonymous access to lawful adult speech
* Avoid chilling effects on expression
* Use the least restrictive means to protect minors
* Avoid identity-based access controls
* Avoid logging or monitoring of viewing behavior

Age checks occur **only** at the point of requesting age-restricted content and reveal **no identity information**.

## Repository Structure

This repository contains:

* A language-agnostic protocol specification
* Formal invariants and threat modeling
* Legal and constitutional design rationale
* A Rust reference implementation demonstrating protocol invariants

The protocol itself is **implementation-independent**.

## Status

This project is currently in **specification and reference implementation** phase.

The protocol invariants are considered **foundational** and must not be altered without a **major version change**.

## License

This repository is published for public review, discussion, and implementation.

Licensing details are specified in the repository root.

