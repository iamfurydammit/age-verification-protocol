# AVP Protocol Invariants (Frozen)

**Status:** FROZEN  
**Applies to:** All implementations, extensions, forks, and integrations  
**Change policy:** Major version change only

---

## 1. Scope Invariant

AVP answers **exactly one question** and no more:

**Is the holder an adult?**

No other attributes may be derived, inferred, revealed, or approximated.

---

## 2. Identity Invariant

AVP MUST NOT provide, infer, or enable:

- Identity
- Pseudonymous identity
- Accounts or profiles
- Persistent identifiers
- Reputation or trust scores

Any system that introduces identity is **out of scope**.

---

## 3. Data Minimization Invariant

AVP MUST NOT retain or expose:

- Date of birth
- Age values
- Names or addresses
- Document numbers
- Biometrics (including face templates, fingerprints, voiceprints)
- Behavioral signals

All personal data used during issuance is **destroyed immediately** after verification.

---

## 4. One-Time Verification Invariant

- Age verification occurs **once**
- No recurring verification is permitted
- No refresh, renewal, or re-check is permitted
- Loss of a token does **not** revoke age eligibility

---

## 5. Time-Based Eligibility Invariant

Adult eligibility is determined solely by a **time-based cryptographic commitment created at issuance**.

The Adult Proof Token contains:

- No date of birth
- No age value
- No counters
- No timestamps
- No clocks
- No update mechanisms

Eligibility emerges **passively** from the passage of time and local proof generation.

No authority, service, contract, or platform may participate in or observe this transition.

---

## 6. Non-Enumerability Invariant

It MUST be cryptographically impossible to:

- Count issued tokens
- Estimate population size
- Infer adoption or usage volume
- Enumerate sessions or users

No global registry, issuance ledger, counter, or observable supply may exist.

---

## 7. Stateless Verification Invariant

Verification MUST be:

- Stateless
- Side-effect free
- Offline-capable

Verification MUST NOT produce:

- Logs
- Counters
- Callbacks
- Telemetry
- Analytics
- Usage signals

---

## 8. No Tracking Invariant

It MUST be cryptographically impossible to determine:

- Whether a token was used
- How often it was used
- Where it was used
- When it was used

This applies to issuers, verifiers, platforms, and third parties.

---

## 9. Client Activation Invariant

The AVP client MUST remain inactive during:

- Normal device use
- OS login
- Application launch
- General web browsing

No age logic, presence logic, timers, or prompts may execute until the user **explicitly requests age-restricted content**.

---

## 10. Explicit Consent Invariant

Adult sessions require **explicit user initiation**.

No background checks, silent elevation, or implicit activation is permitted.

---

## 11. Presence (Not Identity) Invariant

After session entry:

- Identity is never verified
- Age is never re-verified

Only **physical presence and consent** may be confirmed using out-of-band methods.

Failure to confirm presence MUST:

- End the session
- Produce no logs
- Produce no penalties
- Produce no records

---

## 12. Token Locality Invariant

Adult Proof Tokens MUST:

- Be stored locally
- Never be centrally stored
- Never be queryable remotely
- Never be revoked remotely

Tokens are **not** accounts, wallets, or profiles.

---

## 13. Age-Domain Isolation Invariant

Adult and child domains are **mutually exclusive**.

It MUST be impossible for:

- Adult tokens to interact with child tokens
- Child tokens to interact with adult tokens

This applies to:

- Browsing
- Messaging
- Social interaction
- Discovery
- Visibility
- Feeds and replies

Adult users cannot see that child users exist, and vice versa.

---

## 14. Cryptographic Domain Separation Invariant

Adult and child domains share **no cryptographic namespace**.

There MUST be no shared:

- Key space
- Proof system
- Identifier format
- Circuit
- Domain separator
- Trust root

Cross-domain proofs MUST be **structurally invalid and non-representable**, not merely rejected.

---

## 15. No Smart Contracts Invariant

AVP MUST NOT depend on:

- Smart contracts
- Public ledgers
- On-chain state
- Consensus mechanisms
- Observable global state

All eligibility resolution is **local and passive**.

---

## 16. No Central Database Invariant

There MUST be no centralized database of:

- Users
- Tokens
- Ages
- Sessions
- Verifications

Verification artifacts MUST be fragmented such that no single component can reconstruct sensitive data.

---

## 17. Constitutional Narrowness Invariant

AVP MUST:

- Use the least restrictive means to protect minors
- Preserve anonymous access to lawful adult speech
- Avoid chilling effects
- Avoid identity-based access control
- Avoid records of viewing or access behavior

---

## 18. Enforcement Invariant

All guarantees are enforced by **architecture and cryptography**, not by:

- Policy
- Terms of service
- Moderation
- Human review
- Trust assumptions

---

## 19. Change Control Invariant

Any change that violates or weakens these invariants constitutes a **new protocol** and requires a **major version change**.

---

**This document is frozen.**

