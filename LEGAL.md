# Age Verification Protocol (AVP) — Legal & Constitutional Design Rationale

**Status:** Informational  
**Authority:** Subordinate to INVARIANTS.md and PROTOCOL.md  
**Scope:** Legal, constitutional, and regulatory posture  
**Non-goals:** Legal advice, jurisdiction-specific compliance guidance

This document explains the legal and constitutional design rationale of the
Age Verification Protocol (AVP).

Nothing in this document creates legal obligations or supersedes applicable
law. In the event of conflict, `INVARIANTS.md` and `PROTOCOL.md` SHALL prevail.

---

## 1. Purpose and Legal Posture

The Age Verification Protocol (AVP) is designed to enable access to
age-restricted content while:

- Protecting minors
- Preserving anonymous access to lawful adult speech
- Avoiding surveillance, tracking, and identity systems
- Minimizing constitutional risk

AVP is a **technical protocol**, not a regulatory framework, policy system,
or enforcement mechanism.

---

## 2. Constitutional Design Principles (United States)

AVP is designed with explicit consideration of constitutional constraints,
including but not limited to the First and Fourth Amendments.

### 2.1 First Amendment Considerations

Access to lawful adult speech is protected expression.

AVP is designed to:

- Avoid prior restraint
- Avoid content-based discrimination
- Avoid chilling effects on expression
- Avoid identity-based access controls

Age checks occur **only** when a user explicitly requests age-restricted
content. No monitoring occurs outside this context.

---

### 2.2 Least Restrictive Means

AVP implements age gating using the least restrictive technical means by:

- Answering only a single binary question
- Revealing no identity or personal attributes
- Avoiding persistent observation
- Avoiding records of viewing or access behavior

This design minimizes interference with lawful speech while achieving
minor protection objectives.

---

### 2.3 Fourth Amendment Considerations

AVP avoids unreasonable search or surveillance by:

- Performing all checks locally
- Avoiding centralized data collection
- Avoiding persistent identifiers
- Avoiding logs or telemetry

No continuous monitoring or background inspection is performed.

---

## 3. Privacy-by-Architecture

AVP enforces privacy guarantees through **architecture**, not policy.

### 3.1 Data Minimization

AVP processes personal data only once, during issuance, and destroys it
immediately thereafter.

No personal data is retained, aggregated, or reused.

---

### 3.2 No Records Doctrine

AVP is intentionally designed such that:

- No records of access exist
- No usage histories exist
- No activity logs exist

If data does not exist, it cannot be subpoenaed, breached, or abused.

---

## 4. Regulatory Interaction Model

AVP is **regulator-neutral**.

### 4.1 No Built-In Compliance Reporting

AVP does not provide:

- Audit logs
- Usage metrics
- Population statistics
- Behavioral reports

Regulators cannot request information the system does not possess.

---

### 4.2 Non-Enumerability and Legal Requests

Because AVP tokens and usage are non-enumerable:

- Population counts cannot be produced
- Adoption metrics cannot be inferred
- Usage volume cannot be reported

This is a **design constraint**, not a refusal.

---

## 5. Platform and Publisher Neutrality

AVP does not:

- Favor or disfavor platforms
- Impose moderation rules
- Enforce content policy
- Require platform cooperation

Platforms may choose to accept or reject AVP proofs, but AVP does not
mandate integration or behavior.

---

## 6. Liability Containment

### 6.1 No Custodial Role

AVP does not:

- Hold user data
- Store credentials centrally
- Operate accounts
- Control content delivery

This minimizes custodial liability.

---

### 6.2 No Enforcement Authority

AVP does not:

- Enforce laws
- Determine legality of content
- Punish users
- Escalate violations

All enforcement decisions remain external to the protocol.

---

## 7. Jurisdictional Neutrality

AVP is designed to be jurisdiction-agnostic.

The protocol:

- Does not encode age thresholds
- Does not encode legal standards
- Does not assume specific regulatory regimes

Local law determines what constitutes “adult” content and when AVP is used.

---

## 8. Resistance to Abuse and Mission Creep

AVP is intentionally narrow to resist expansion into:

- Identity systems
- Social credit systems
- Surveillance tooling
- Content control mechanisms

Frozen invariants and a closed protocol surface prevent silent expansion.

---

## 9. Non-Compliance and Misrepresentation

Any system that introduces:

- Identity
- Tracking
- Enumeration
- Surveillance
- Centralized control

is **not AVP** and MUST NOT claim compatibility with AVP.

---

## 10. Disclaimer

This document is not legal advice.

AVP is a technical protocol. Adoption, deployment, and legal compliance
remain the responsibility of implementers and operators.

---

**End of Legal & Constitutional Design Rationale**
