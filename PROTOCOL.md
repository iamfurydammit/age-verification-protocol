# Age Verification Protocol (AVP) — Protocol Specification

**Status:** Draft (Subordinate to INVARIANTS.md)  
**Scope:** Normative protocol behavior  
**Non-goals:** Implementation, optimization, extensions

This document specifies the behavior of the Age Verification Protocol (AVP).

All behavior described herein is constrained by and subordinate to
`INVARIANTS.md`. In the event of conflict, `INVARIANTS.md` SHALL prevail.

---

## 1. Actors

The protocol defines the following actors.

### 1.1 User

A natural person seeking access to age-restricted content.

The protocol does not identify, name, profile, or persistently recognize the user.

---

### 1.2 Issuance System

A one-time verification environment responsible solely for determining whether
the user is an adult at the time of issuance.

The Issuance System MUST NOT:

- retain personal data after issuance
- issue revocable or enumerable credentials
- observe post-issuance usage

---

### 1.3 Client

Local software under the user’s control that:

- stores the Adult Proof Token
- generates zero-knowledge proofs
- enforces local session boundaries

The Client is passive by default.

---

### 1.4 Verifier

A stateless system operated by an age-restricted service that:

- receives a proof
- verifies it
- learns only whether the user is an adult

The Verifier MUST NOT:

- log proofs
- correlate requests
- retain state

---

## 2. Protocol Artifacts

### 2.1 Adult Proof Token (APT)

A non-transferable, non-enumerable, locally stored credential issued once
to an adult user.

The APT:

- is not an account or identity
- contains no date of birth, age value, or timestamps
- cannot be queried or revoked remotely
- supports local zero-knowledge proof generation

---

### 2.2 Zero-Knowledge Proof

A locally generated proof that answers exactly one question:

**“Is the holder an adult?”**

The proof reveals no additional information and produces no side effects.

---

## 3. Protocol Phases

The protocol consists of four phases:

1. Issuance  
2. Storage  
3. Session Entry  
4. Verification  

Each phase is strictly ordered and non-overlapping.
## 4. Issuance Phase

The Issuance Phase is the only phase in which personal data is processed.

Issuance occurs exactly once per user and results in the creation of a single
Adult Proof Token (APT).

---

### 4.1 Preconditions

Issuance MUST occur only when all of the following conditions are met:

- The user explicitly initiates issuance
- The Issuance System is operating in a one-time verification mode
- No prior Adult Proof Token exists for the issuance context

Issuance MUST NOT occur automatically, silently, or in the background.

---

### 4.2 Inputs

The Issuance System MAY receive the following inputs:

- Government-issued identification sufficient to determine date of birth
- A one-time proof-of-life signal sufficient to confirm a live human presence

Inputs are used **solely** to determine whether the user is an adult at the
moment of issuance.

No additional attributes may be derived.

---

### 4.3 Verification Constraint

The Issuance System MUST:

- Determine adult status only
- Ignore identity, name, address, or document identifiers
- Avoid creating persistent identifiers or correlatable artifacts

The Issuance System MUST NOT:

- Store date of birth
- Store age values
- Store biometric templates
- Store raw identification data
- Perform recurring or scheduled checks

---

### 4.4 Cryptographic Commitment Creation

Upon successful verification that the user is an adult, the Issuance System
MUST create a cryptographic commitment sufficient to enable future adult
eligibility determination through the passage of time alone.

The commitment MUST:

- Contain no date of birth
- Contain no age value
- Contain no timestamps
- Contain no counters
- Contain no clocks
- Contain no update mechanisms

The commitment MUST be suitable for local, stateless proof generation.

---

### 4.5 Token Construction

The Adult Proof Token (APT) MUST be constructed using the cryptographic
commitment produced during issuance.

The APT MUST:

- Be non-transferable
- Be non-enumerable
- Be unlinkable to issuance artifacts
- Be suitable for local storage
- Support zero-knowledge proof generation

The APT MUST NOT:

- Encode identity
- Encode age or date of birth
- Be queryable remotely
- Be revocable remotely

---

### 4.6 Artifact Destruction

Immediately upon successful issuance:

- All personal data inputs MUST be destroyed
- All intermediate artifacts MUST be destroyed
- No recovery, audit, or escrow copies may exist

Destruction MUST occur before the Issuance System becomes inactive.

---

### 4.7 Post-Issuance State

After issuance completes:

- The Issuance System MUST become observationally irrelevant
- The Issuance System MUST NOT observe or influence any future protocol phase
- The APT MUST exist solely under user control

Any system behavior after issuance is outside the Issuance Phase.
