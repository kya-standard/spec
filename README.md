# KYA — Know Your Agent
### Open Standard for AI Agent Identity and Governance

KYA is an open standard for establishing verifiable identity,
behavioral accountability, and tamper-evident audit trails for
autonomous AI agents.

**Observable is not provable. KYA makes agent behavior provable.**

## Documents

| Document | Description |
|----------|-------------|
| KYA-SPEC-v1.0.1.md | Full specification |
| CHAIN-SPEC.md | Cryptographic chain specification |
| WHITEPAPER.md | The case for an open governance standard |

## Chain Verification (30 lines of Python)

```python
import hashlib, json

def canonical_json(obj):
    return json.dumps(
        obj, sort_keys=True, separators=(',', ':'), ensure_ascii=False
    ).encode('utf-8')

def verify_chain(events):
    prev_hash = None
    for i, event in enumerate(events):
        if event.get('chain_index') != i:
            return False, i, "missing chain_index"
        if event.get('previous_event_hash') != prev_hash:
            return False, i, "chain link broken"
        event_copy = {k: v for k, v in event.items() if k != 'event_hash'}
        computed = hashlib.sha256(canonical_json(event_copy)).hexdigest()
        if computed != event.get('event_hash'):
            return False, i, "event modified"
        prev_hash = event['event_hash']
    return True, None, "chain valid"


