# Age Verification Protocol (AVP) — Threat Model

**Status:** Informational (Subordinate to INVARIANTS.md and PROTOCOL.md)  
**Scope:** Adversarial analysis and risk assessment  
**Non-goals:** Policy, enforcement, implementation guidance

This document identifies and analyzes threats to the Age Verification
Protocol (AVP) and explains how protocol design mitigates them.

This document does not introduce requirements. In the event of conflict,
`INVARIANTS.md` and `PROTOCOL.md` SHALL prevail.

---

## 1. Threat Model Assumptions

The following assumptions define the adversarial environment.

### 1.1 Adversary Capabilities

Adversaries MAY:

- Control networks
- Observe traffic
- Operate malicious platforms
- Operate malicious verification services
- Attempt correlation and inference attacks
- Attempt replay or substitution attacks
- Attempt enumeration or population inference
- Attempt social engineering

Adversaries MAY be:

- External attackers
- Platforms
- Issuers
- Verifiers
- Governments
- Commercial data aggregators

---

### 1.2 Trusted Components

The protocol assumes trust only in:

- The user’s local device for execution correctness
- The Issuance System *only during issuance*
- Cryptographic soundness of proof systems

No trust is assumed after issuance.

---

## 2. Threat Categories

Threats are categorized as follows:

1. Identity Disclosure
2. Tracking and Surveillance
3. Enumeration and Population Inference
4. Cross-Domain Interaction
5. Token Theft or Misuse
6. Platform Abuse
7. Issuer or Verifier Misconduct
8. Network-Level Attacks
9. Legal and Regulatory Abuse
10. Implementation Errors

---

## 3. Identity Disclosure Threats

### 3.1 Threat: User Identification via Proofs

**Description:**  
A verifier attempts to identify a user based on proof contents or structure.

**Mitigation:**  
- Proofs contain no identifiers
- Proofs are unlinkable
- Proofs answer exactly one question
- Verifiers are stateless

**Residual Risk:**  
None at the protocol level.

---

### 3.2 Threat: Identity Reconstruction via Issuance Artifacts

**Description:**  
An attacker attempts to reconstruct identity from issuance records.

**Mitigation:**  
- Issuance artifacts are destroyed immediately
- No persistent identifiers are created
- Verification artifacts are fragmented

**Residual Risk:**  
Limited to issuance compromise during issuance only.

---

## 4. Tracking and Surveillance Threats

### 4.1 Threat: Usage Tracking by Verifiers

**Description:**  
A verifier attempts to log or correlate proof usage.

**Mitigation:**  
- Stateless verification
- No session identifiers
- No timestamps
- No counters

**Residual Risk:**  
Out-of-protocol logging by a malicious verifier (non-compliant behavior).

---

### 4.2 Threat: Background Monitoring by Client

**Description:**  
A client implementation attempts to monitor user behavior.

**Mitigation:**  
- Client activation boundary
- Explicit session entry requirement
- No background activity permitted

**Residual Risk:**  
Malicious client implementations (non-compliant).

---

## 5. Enumeration and Population Inference Threats

### 5.1 Threat: Counting Issued Tokens

**Description:**  
An adversary attempts to infer the number of adults using the system.

**Mitigation:**  
- No issuance ledger
- Non-enumerable tokens
- No global registry

**Residual Risk:**  
None at the protocol level.

---

### 5.2 Threat: Verification Volume Analysis

**Description:**  
An adversary attempts to infer population size via verification frequency.

**Mitigation:**  
- Stateless verification
- No counters
- No observable supply

**Residual Risk:**  
Traffic analysis outside protocol scope.

---

## 6. Cross-Domain Interaction Threats

### 6.1 Threat: Adult–Child Interaction

**Description:**  
An attacker attempts to bridge adult and child domains.

**Mitigation:**  
- Strict age-domain isolation
- No shared cryptographic namespace
- Structural non-representability of cross-domain proofs

**Residual Risk:**  
None by design.

---

### 6.2 Threat: Downgrade or Upgrade Attacks

**Description:**  
An attacker attempts to coerce a token into the wrong domain.

**Mitigation:**  
- Separate proof systems
- Separate verification contexts
- Explicit domain separation

**Residual Risk:**  
None by design.

---

## 7. Token Theft and Misuse Threats

### 7.1 Threat: Token Theft

**Description:**  
An attacker steals a device containing an Adult Proof Token.

**Mitigation:**  
- Local storage only
- Optional local access controls
- No remote usability without possession

**Residual Risk:**  
Equivalent to device compromise.

---

### 7.2 Threat: Token Duplication

**Description:**  
An attacker attempts to copy or clone a token.

**Mitigation:**  
- Non-transferability
- Local binding
- No remote enumeration

**Residual Risk:**  
Implementation-dependent.

---

## 8. Platform Abuse Threats

### 8.1 Threat: Platform-Based Identity Linking

**Description:**  
A platform attempts to correlate AVP usage with user accounts.

**Mitigation:**  
- No identifiers in proofs
- No session IDs
- Stateless verification

**Residual Risk:**  
Platform policy violations (outside protocol).

---

### 8.2 Threat: Forced Account Creation

**Description:**  
A platform requires identity to access adult content.

**Mitigation:**  
- AVP does not support identity
- Such systems are non-compliant with AVP

**Residual Risk:**  
Regulatory or policy coercion.

---

## 9. Issuer and Verifier Misconduct

### 9.1 Threat: Malicious Issuer

**Description:**  
An issuer logs or retains personal data.

**Mitigation:**  
- One-time issuance
- Immediate artifact destruction
- No post-issuance authority

**Residual Risk:**  
Trust violation during issuance only.

---

### 9.2 Threat: Malicious Verifier

**Description:**  
A verifier attempts to log or correlate proofs.

**Mitigation:**  
- Stateless design
- No usable proof metadata

**Residual Risk:**  
Out-of-protocol behavior.

---

## 10. Network-Level Attacks

### 10.1 Threat: Traffic Analysis

**Description:**  
An adversary observes network traffic patterns.

**Mitigation:**  
- Proofs reveal no information
- No persistent identifiers

**Residual Risk:**  
General internet metadata leakage (out of scope).

---

### 10.2 Threat: Replay Attacks

**Description:**  
An attacker replays a previously captured proof.

**Mitigation:**  
- Proof freshness enforced locally
- Verifier statelessness limits usefulness

**Residual Risk:**  
Implementation-dependent safeguards.

---

## 11. Legal and Regulatory Abuse Threats

### 11.1 Threat: Mandated Backdoors

**Description:**  
A government attempts to require tracking or identification.

**Mitigation:**  
- Architecture does not support tracking
- No observable state exists to provide

**Residual Risk:**  
Legal coercion outside protocol scope.

---

### 11.2 Threat: Compelled Enumeration

**Description:**  
A regulator demands population metrics.

**Mitigation:**  
- Non-enumerability by design
- No data exists to provide

**Residual Risk:**  
None at protocol level.

---

## 12. Implementation Errors

### 12.1 Threat: Accidental Logging

**Description:**  
An implementation logs data unintentionally.

**Mitigation:**  
- Explicit prohibitions
- Stateless design
- Compliance rules

**Residual Risk:**  
Developer error.

---

### 12.2 Threat: Scope Creep

**Description:**  
Future contributors add features that violate invariants.

**Mitigation:**  
- Frozen invariants
- Closed protocol surface
- Explicit non-compliance consequences

**Residual Risk:**  
Governance failure.

---

## 13. Summary

The Age Verification Protocol is designed to:

- Minimize trust
- Eliminate observability
- Prevent enumeration
- Prevent identity leakage
- Prevent cross-domain interaction

Residual risks are limited to:
- Device compromise
- Malicious implementations
- Legal coercion outside protocol control

These risks are explicitly out of scope and do not weaken protocol guarantees.

---

**End of Threat Model**
