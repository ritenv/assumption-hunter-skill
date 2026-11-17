# Assumption classification guide

Use these examples to calibrate findings, not as exhaustive rules.

| Situation | Classification | Recommended response |
| --- | --- | --- |
| User explicitly requires PostgreSQL; plan uses PostgreSQL | Confirmed | No flag |
| User requests a simple button; agent chooses existing component style | Reasonable default | Proceed |
| User requests CSV export; agent assumes only visible rows should export | Unverified | Check requirements; clarify if outcome changes materially |
| User says all filtered results must export; agent exports current page only | Contradicted | Flag and correct proposal |
| Payment endpoint assumes webhook events arrive exactly once | Unverified, high impact | Require idempotency design and evidence |
| Data deletion request doesn't specify soft vs permanent deletion, with regulatory implications | Blocking ambiguity | Ask before destructive action |
| User asks to change copy; agent assumes database migration needed | Unverified | Challenge unnecessary implementation |
| Documentation states API pagination is cursor-based and source confirms it | Confirmed | No flag |

## Evidence hierarchy

1. Current explicit user instructions and approved decisions.
2. Directly inspected code, tests, schemas, logs, or authoritative specifications.
3. Reliable external documentation when available and relevant.
4. Project conventions supported by repeated examples.
5. General conventions and model inference (not independent verification).

Evidence can conflict; flag inconsistencies instead of silently selecting the convenient source. Newer instructions may supersede older decisions, but only within their stated scope.

## Materiality prompts

- What observable behavior changes if this assumption is false?
- Could it expose data, cause financial loss, or create irreversible changes?
- Would a different interpretation substantially change architecture or user experience?
- Can we cheaply inspect a file, run a test, or ask one precise question?
- Can we proceed with a reversible choice while explicitly noting uncertainty?

## False-positive controls

Do not flag every unspecified detail. Prefer at most 3–5 high-impact findings unless asked for exhaustive review. Avoid questions about defaults that are easily changed and unlikely to affect correctness. An empty audit is a valid result.
