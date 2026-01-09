# Age Verification Protocol (AVP) — Protocol Specification

**Status:** Draft (Subordinate to INVARIANTS.md)  
**Scope:** Normative protocol behavior  
**Non-goals:** Implementation, optimization, extensions

This document specifies the behavior of the Age Verification Protocol (AVP).

All behavior described herein is constrained by and subordinate to
`INVARIANTS.md`. In the event of conflict, `INVARIANTS.md` SHALL prevail.
## 1. Actors

The protocol defines the following actors:

### 1.1 User

A natural person seeking access to age-restricted content.

The protocol does not identify, name, profile, or persistently recognize
the user.

### 1.2 Issuance System

A one-time verification environment responsible solely for determining
whether the user is an adult at the time of issuance.

The Issuance System MUST NOT:
- retain personal data after issuance
- issue revocable or enumerable credentials
- observe post-issuance usage

### 1.3 Client

Local software under the user’s control that:
- stores the Adult Proof Token
- generates zero-knowledge proofs
- enforces local session boundaries

The Client is passive by default.

### 1.4 Verifier

A stateless system operated by an age-restricted service that:
- receives a proof
- verifies it
- learns only whether the user is an adult

The Verifier MUST NOT:
- log proofs
- correlate requests
- retain state
## 2. Protocol Artifacts

### 2.1 Adult Proof Token (APT)

A non-transferable, non-enumerable, locally stored credential issued once
to an adult user.

The APT:
- is not an account or identity
- contains no DOB, age value, or timestamps
- cannot be queried or revoked remotely
- supports local zero-knowledge proof generation

### 2.2 Zero-Knowledge Proof

A locally generated proof that answers exactly one question:

“Is the holder an adult?”

The proof reveals no additional information and produces no side effects.
## 3. Protocol Phases

The protocol consists of four phases:

1. Issuance
2. Storage
3. Session Entry
4. Verification

Each phase is strictly ordered and non-overlapping.
