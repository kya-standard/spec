# KYA Chain Specification
## Cryptographic Hash Chain for AI Agent Audit Trails
**Version:** 1.0.0
**Part of:** KYA — Know Your Agent Standard
**License:** MIT

## Overview

The chain has one property that matters above all others:
self-verifying. Any party with a chain export can verify
its integrity without calling any API, contacting any server,
or trusting any third party. The math is the proof.

## Design Principles

Append-only: Events are never modified or deleted.
Per-agent: Each agent has its own independent chain.
No raw content: Hashes only, never payloads.
Minimal dependencies: SHA-256 only.
Gap-inclusive: Offline periods are explicit events.

## Canonical JSON Rules

1. Keys sorted alphabetically, recursively.
2. No whitespace.
3. UTF-8 encoding.
4. Strings use double quotes.
5. Numbers use minimal representation.
6. No trailing commas.
7. Null values included as null.
8. Arrays preserve original order.

## Reference Implementation (Python)

import json

def canonical_json(obj):
    return json.dumps(
        obj,
        sort_keys=True,
        separators=(',', ':'),
        ensure_ascii=False
    ).encode('utf-8')

## Reference Implementation (Node.js)

function sortedJson(obj) {
  if (typeof obj !== 'object' || obj === null) return obj;
  if (Array.isArray(obj)) return obj.map(sortedJson);
  return Object.keys(obj).sort().reduce((acc, key) => {
    acc[key] = sortedJson(obj[key]);
    return acc;
  }, {});
}

function canonicalJson(obj) {
  return Buffer.from(JSON.stringify(sortedJson(obj)), 'utf-8');
}

## Hash Computation

input_hash  = SHA-256(canonical_json(input_payload))
output_hash = SHA-256(canonical_json(output_payload))
event_hash  = SHA-256(canonical_json(event_excluding_event_hash))

## Chain Linking

Event 0: previous_event_hash = null (genesis)
Event 1: previous_event_hash = event_hash(Event 0)
Event N: previous_event_hash = event_hash(Event N-1)

## Chain Verification (Python)

import hashlib, json

def verify_chain(events):
    prev_hash = None
    for i, event in enumerate(events):
        stored_hash = event['event_hash']
        event_copy = {k: v for k, v in event.items()
                      if k != 'event_hash'}
        computed = hashlib.sha256(
            canonical_json(event_copy)
        ).hexdigest()
        if computed != stored_hash:
            return False, i, "event_hash mismatch"
        if event['previous_event_hash'] != prev_hash:
            return False, i, "chain link broken"
        prev_hash = stored_hash
    return True, None, "chain valid"

## Chain Export Format

JSON array of events in ascending chain_index order.
File naming: kya-chain-{agent_id}-{start}-{end}.json

## Tamper Evidence Properties

Forward Integrity: Modifying event N invalidates all after N.
Insertion Resistance: Insertions produce detectable divergence.
Deletion Resistance: Deletions break the chain at next link.

*KYA Chain Specification v1.0.0*
*Part of the KYA open standard. MIT License.*
*Authored by Rankigi Inc. | rankigi.com/standard*
