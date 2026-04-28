# KYA — Know Your Agent
## Open Standard for AI Agent Identity and Governance
**Version:** 1.0.1
**Status:** Draft
**Authored by:** Rankigi Inc.
**License:** MIT

## Abstract

KYA is an open standard for establishing verifiable identity,
behavioral accountability, and tamper-evident audit trails for
autonomous AI agents. Implementation-agnostic. MIT licensed.

## 1. Motivation

Observable is not provable. KYA makes agent behavior provable.

Logs can be edited. Dashboards show what agents report. Neither
proves what agents did. KYA provides a cryptographic record made
at the moment of action by a system the agent cannot influence.

## 2. Scope

KYA defines:
1. The Agent Passport
2. The governed event schema
3. The hash chain rules
4. The snapshot format
5. The verification protocol
6. The issuer authority model (X.509 PKI)

## 3. Agent Passport

Every KYA-governed agent receives a passport at birth.

### 3.1 Required Fields

passport_id, agent_id, agent_name, issued_at, issuer,
public_key (Ed25519), genesis_event_hash, scope, status,
passport_hash

### 3.5 Issuer Authority (X.509)

KYA adopts X.509 PKI for issuer authority verification.
Three levels: Root CA (offline) > Intermediate CA (online) >
Agent Passport Certificate (per agent at birth).

Additional fields: passport_certificate (PEM), issuer_ca_url,
issuer_ca_fingerprint, certificate_serial,
certificate_not_before, certificate_not_after.

Verification (no network required if certs held):
openssl verify -CAfile root-ca.pem -untrusted intermediate-ca.pem passport-certificate.pem

## 4. Event Schema

Client fields: event_id, agent_id, timestamp, action_type,
tool_invoked, input_hash, output_hash, decision_metadata,
execution_result, data_quality_flag

Ledger fields (server-computed): server_received_at,
previous_event_hash, chain_index, event_hash

## 5. Offline Gap Detection

Gaps are governed events. Default threshold: 15 minutes.
agent_offline_start and agent_offline_end events created.

## 6. Hash Chain Rules

Canonical JSON: keys sorted alphabetically, no whitespace, UTF-8.

event_hash = SHA-256(canonical_json(event excluding event_hash))
previous_event_hash links each event to the prior one.

Verification requires no external service.

## 7. Daily Snapshot

snapshot_hash = SHA-256(canonical_json(snapshot payload))
External anchoring via Sigstore Rekor optional.

## 8. Compliance Mapping

SHA-256 hash chain satisfies tamper-evident record requirements.
X.509 certificate chain satisfies issuer authority verification.
Covers: SOC 2 CC7.1, EU AI Act Art. 13 and 14, HIPAA 164.312(b).

## 9. Conformance Levels

KYA Basic: Passport, event schema, hash chain, local verification.
KYA Standard: Adds offline detection, snapshots, X.509.
KYA Extended: Full PKI, CRL/OCSP, federation, regulation exports.

## 10. Versioning

Version 1.0.1. See CHAIN-SPEC.md for full cryptographic detail.

## 11. Reference Implementation

https://github.com/Rankigi-Inc/governed-agent-core
Public verification: https://verify.rankigi.com

## 12. Contributing

This repo: https://github.com/kya-standard/spec
Gaps in the spec are bugs. Open an issue.

*MIT License. Free to implement, extend, and distribute.*
*Authored by Rankigi Inc. | rankigi.com/standard*
