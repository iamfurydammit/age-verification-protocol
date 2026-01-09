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
## 5. Storage Phase

The Storage Phase governs how the Adult Proof Token (APT) is retained after
issuance.

The Storage Phase is entirely local and does not involve any networked system.

---

### 5.1 Storage Location

The Adult Proof Token MUST:

- Be stored locally on a device under the user’s control
- Never be stored in a centralized or remote system
- Never be replicated to a shared or observable location

The protocol does not mandate a specific storage mechanism.

---

### 5.2 Access Control

Access to the Adult Proof Token MAY be gated by local device security
mechanisms.

Such mechanisms MAY include:

- Device authentication
- Local application authentication
- Secure hardware enclaves

Access controls MUST NOT:

- Introduce identity
- Introduce persistent identifiers
- Introduce network dependencies

---

### 5.3 Network Isolation

During the Storage Phase:

- The Adult Proof Token MUST NOT be transmitted
- The Adult Proof Token MUST NOT be synchronized
- The Adult Proof Token MUST NOT be queried remotely

No background network activity may occur as a result of token storage.

---

### 5.4 Enumeration Resistance

Storage of the Adult Proof Token MUST NOT enable:

- Counting of tokens
- Estimation of population size
- Discovery of other tokens
- Correlation across devices or users

There MUST be no global index, registry, or namespace associated with storage.

---

### 5.5 Loss and Destruction

Loss or destruction of the Adult Proof Token:

- Does NOT revoke age eligibility
- Does NOT trigger any remote notification
- Does NOT create a record or signal

The protocol does not guarantee recoverability of a lost token.

---

### 5.6 Re-Issuance After Loss

If a token is lost, the user MAY re-enter the Issuance Phase.

Re-issuance:

- MUST follow the same constraints as initial issuance
- MUST NOT rely on prior issuance records
- MUST NOT assume continuity or identity

Each issuance is independent.

---

### 5.7 Storage Phase Boundaries

The Storage Phase ends when the user explicitly initiates a session to access
age-restricted content.

No session state exists during the Storage Phase.
## 6. Session Entry Phase

The Session Entry Phase governs the explicit activation of an adult session
for the purpose of accessing age-restricted content.

No session exists prior to this phase.

---

### 6.1 Activation Boundary

The Client MUST remain inactive until the user explicitly initiates an adult
session.

The Client MUST NOT perform any of the following prior to explicit session
initiation:

- Age checks
- Presence checks
- Timers or countdowns
- Background prompts
- Silent elevation
- Pre-fetching of age-restricted content

---

### 6.2 Explicit User Action

Session Entry MUST be triggered by a deliberate user action indicating intent
to access age-restricted content.

The protocol does not permit:

- Automatic session initiation
- Passive inference of intent
- Session initiation based on browsing patterns

---

### 6.3 Session Entry Preconditions

A session MAY be initiated only if:

- An Adult Proof Token is locally available
- The Client is operating in a non-session state
- The user has explicitly requested access to age-restricted content

No other preconditions are permitted.

---

### 6.4 Entry Confirmation

Session Entry MAY require one or more local or out-of-band confirmations to
establish present user consent.

Permissible confirmation mechanisms include:

- Local device authentication
- One-time email confirmation
- One-time SMS confirmation
- Hardware-based confirmation

Confirmation mechanisms:

- MUST NOT establish identity
- MUST NOT persist identifiers
- MUST NOT be used for tracking or presence monitoring

---

### 6.5 Session Creation

Upon successful confirmation:

- A local adult session MUST be created
- The session MUST exist only within the Client
- No session identifier may be transmitted externally

The session represents **consent and presence**, not identity.

---

### 6.6 Failure Handling

If session entry confirmation fails:

- No session MUST be created
- No retry counters MUST be stored
- No penalties or flags MUST be recorded
- No observable signal MUST be emitted

The Client MUST return to a non-session state.

---

### 6.7 Session Entry Phase Boundaries

The Session Entry Phase ends immediately upon:

- Successful session creation, or
- Failure to confirm session entry

No age-restricted content may be accessed outside an active session.
## 7. Verification Phase

The Verification Phase governs how age-restricted content access is authorized
using a zero-knowledge proof.

Verification occurs only within an active adult session.

---

### 7.1 Verification Trigger

Verification MUST occur only when:

- The user is within an active adult session
- Age-restricted content has been explicitly requested

Verification MUST NOT occur:

- During general browsing
- Prior to explicit content request
- Outside an active session

---

### 7.2 Proof Generation

Upon a verification trigger:

- The Client MUST generate a zero-knowledge proof locally
- Proof generation MUST use only the Adult Proof Token
- Proof generation MUST produce no side effects

The proof MUST answer exactly one question:

**“Is the holder an adult?”**

No additional attributes may be encoded or inferred.

---

### 7.3 Proof Transmission

The Client MAY transmit the proof to a Verifier solely for the purpose of
verification.

The transmitted proof MUST:

- Contain no identifiers
- Contain no timestamps
- Contain no session identifiers
- Be unlinkable to prior proofs

The Client MUST NOT transmit the Adult Proof Token itself.

---

### 7.4 Verifier Behavior

Upon receiving a proof, the Verifier MUST:

- Verify the proof statelessly
- Learn only whether the proof is valid
- Produce a binary outcome: valid or invalid

The Verifier MUST NOT:

- Log the proof
- Retain the proof
- Correlate requests
- Count verifications
- Infer session duration or frequency

---

### 7.5 Content Gating

Age-restricted content MUST NOT be transmitted unless verification succeeds.

Verification outcomes MUST be enforced as follows:

- Valid proof → content MAY be delivered
- Invalid or absent proof → content MUST NOT be transmitted

Users MUST NOT receive partial, preview, or degraded versions of restricted
content prior to successful verification.

---

### 7.6 Failure Handling

If verification fails:

- No retry counters MUST be stored
- No penalties or flags MUST be recorded
- No observable signal MUST be emitted

The session MAY continue, but access to age-restricted content remains denied.

---

### 7.7 Verification Phase Boundaries

The Verification Phase ends immediately upon:

- Successful verification and content delivery decision, or
- Verification failure

Verification does not extend session duration and does not refresh eligibility.
## 8. Phase Transitions and Invalid States

This section defines the complete and exclusive set of legal phase
transitions within the Age Verification Protocol (AVP).

Any behavior not explicitly permitted by this section is invalid.

---

### 8.1 Protocol States

The protocol operates in exactly one of the following states at any time:

1. No Token
2. Stored
3. Session Pending
4. Session Active
5. Verification In Progress

No additional states are permitted.

---

### 8.2 Legal State Transitions

The following transitions are the only legal transitions:

- No Token → Stored  
  (Successful completion of Issuance Phase)

- Stored → Session Pending  
  (User explicitly initiates Session Entry)

- Session Pending → Session Active  
  (Successful session entry confirmation)

- Session Pending → Stored  
  (Session entry fails or is abandoned)

- Session Active → Verification In Progress  
  (Age-restricted content is requested)

- Verification In Progress → Session Active  
  (Verification completes, regardless of outcome)

- Session Active → Stored  
  (Session ends or presence confirmation fails)

No other transitions are permitted.

---

### 8.3 Prohibited Transitions

The following transitions are explicitly forbidden:

- No Token → Session Pending
- No Token → Session Active
- No Token → Verification In Progress
- Stored → Session Active
- Stored → Verification In Progress
- Verification In Progress → Stored
- Verification In Progress → No Token

Any implementation that permits a prohibited transition is non-compliant.

---

### 8.4 Invalid State Handling

If an invalid state or transition is detected:

- The Client MUST terminate the current operation
- The Client MUST revert to the last valid state
- No logs, counters, or error records MUST be persisted
- No network signals MUST be emitted

Invalid state detection MUST NOT trigger penalties or lockouts.

---

### 8.5 Session Termination Semantics

Session termination occurs when:

- The user explicitly ends the session
- Presence confirmation fails
- The Client exits or resets
- Session continuity is lost

Upon termination:

- The state MUST transition to Stored
- No residual session state may persist
- No verification state may persist

---

### 8.6 Token Loss Semantics

If the Adult Proof Token becomes unavailable:

- The state MUST transition to No Token
- No revocation signal MUST be emitted
- No record of loss MUST be stored

Token loss does not affect eligibility and does not propagate externally.

---

### 8.7 Undefined Behavior Prohibition

Any behavior not defined by Sections 4 through 8 is undefined and prohibited.

Implementations MUST NOT:

- Invent fallback behavior
- Infer missing transitions
- Extend the state machine implicitly
## 9. Global Prohibitions and Compliance Rules

This section defines protocol-wide prohibitions and compliance requirements.

These rules apply to all actors, phases, and implementations of AVP.

---

### 9.1 Identity Prohibition

Implementations MUST NOT:

- Create or require user accounts
- Assign persistent identifiers
- Infer or store identity
- Link tokens to real-world persons
- Introduce pseudonymous tracking

Any implementation that introduces identity is non-compliant.

---

### 9.2 Tracking and Observation Prohibition

Implementations MUST NOT:

- Log proof usage
- Record access attempts
- Count sessions or verifications
- Measure frequency or duration
- Emit analytics or telemetry

Observability by issuers, verifiers, platforms, or third parties is prohibited.

---

### 9.3 Enumeration Prohibition

Implementations MUST NOT:

- Maintain issuance counters
- Maintain verification counters
- Maintain global registries
- Estimate population size
- Infer adoption metrics

Tokens, sessions, and users MUST remain non-enumerable.

---

### 9.4 Network and Ledger Prohibition

Implementations MUST NOT depend on:

- Smart contracts
- Public or private ledgers
- Consensus systems
- On-chain state
- Global clocks or timestamps

All eligibility resolution MUST remain local and passive.

---

### 9.5 Cryptographic Scope Limitation

Implementations MUST NOT:

- Extend proofs beyond adult / not adult
- Encode auxiliary attributes
- Support multi-attribute queries
- Allow attribute aggregation

Any proof answering more than one question is invalid.

---

### 9.6 Session Scope Limitation

Implementations MUST NOT:

- Persist session identifiers
- Share session state externally
- Extend sessions implicitly
- Refresh eligibility through session activity

Sessions represent consent and presence only.

---

### 9.7 Recovery and Escrow Prohibition

Implementations MUST NOT:

- Provide centralized recovery services
- Escrow tokens or commitments
- Retain backup copies
- Offer revocation or reactivation APIs

Loss of a token does not create recovery obligations.

---

### 9.8 Platform Neutrality Requirement

Implementations MUST NOT:

- Favor specific platforms
- Require platform cooperation
- Impose integration obligations
- Enforce content policy

AVP is content-agnostic and platform-neutral.

---

### 9.9 Compliance Determination

An implementation is compliant with AVP if and only if:

- All invariants in `INVARIANTS.md` are upheld
- All protocol behavior in `PROTOCOL.md` is implemented without extension
- No prohibited behavior is present

Partial compliance is not permitted.

---

### 9.10 Non-Compliance Consequence

Any implementation that violates these rules:

- Is not AVP
- MUST NOT claim AVP compatibility
- MUST NOT reuse the AVP name or identifiers
