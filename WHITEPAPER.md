# Why AI Agents Need an Open Governance Standard
## The Case for KYA — Know Your Agent
**Rankigi Inc. | 2026**
**License:** Creative Commons CC-BY 4.0

## Abstract

Autonomous AI agents are executing real-world actions at scale.
The infrastructure governing these actions has not kept pace
with their capabilities.

The governance gap is structural. It cannot be solved by better
dashboards or improved observability tooling. It requires a
cryptographic standard that makes agent behavior provable,
not merely visible.

## 1. The Problem Is Not Visibility

The default assumption is that observability is governance.
This is wrong.

Logs can be edited. Databases can be updated. Dashboards show
what systems report, not what systems did. The gap between
what was reported and what happened is permanent without a
tamper-evident record made at the time of the action.

## 2. The Volkswagen Effect

In 2015, Volkswagen programmed engines to behave differently
during testing. AI agents exhibit an analogous property.

An agent observed through its own reporting layer shows what
it chooses to report. This is not governance. This is the
agent governing itself.

Genuine governance requires independence. The audit trail must
be produced by a system the agent cannot influence.

## 3. The Pattern Has Worked Before

Double-entry bookkeeping: every transaction in two places.
Discrepancies are immediately detectable.

Supply chain attestation: cryptographic records proving what
code was built, when, from what source.

TLS: a protocol, not a product. Any conforming implementation
can establish a secure connection with any other. Security
comes from the protocol, not trust in any vendor.

KYA is designed on the same principle.

## 4. Why Proprietary Governance Fails

If your audit trail is stored in a vendor proprietary format,
verifiable only through vendor tools, your audit trail is only
as trustworthy as your relationship with that vendor.

A KYA chain export from 2026 can be verified in 2036 with
nothing more than a SHA-256 library and this specification.

## 5. The Notary Model

Every governance framework defines what agents should do.
None of them can prove what agents did.

A policy document and a cryptographic record are different
legal objects. Both are required. Neither replaces the other.

A notary does not tell you what contract to sign. They witness
the signing and certify it occurred. Every legal system trusts
the notary because the notary has no stake in the outcome.

RANKIGI is the notary for AI agent execution.

## 6. The Timing Argument

The EU AI Act, NIST AI RMF, and state-level AI legislation
are defining what constitutes adequate audit evidence for
AI agent actions right now.

The organizations that provide concrete technical answers
during this definition period will shape what adequate means.

## 7. Call for Participation

KYA is an open standard. The specification is published at:
https://github.com/kya-standard/spec

We are seeking technical review, implementation feedback,
regulatory alignment review, and extension proposals.

If you find a gap in the spec, that gap is a bug.

---

*Rankigi Inc. | rankigi.com | kya-standard.org*
*CC-BY 4.0. KYA Specification: MIT License.*
