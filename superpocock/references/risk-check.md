# SuperPocock risk check

Run this check after the problem or design is understood and before detailed planning. It is a routing gate, not a numeric quality score.

## High-risk dimensions

Use the deep path when any answer is **yes** or materially uncertain.

| Dimension | High-risk signal |
| --- | --- |
| Identity and ownership | The change decides who owns data, how entities are matched, or how duplicate identities are prevented. |
| Authorization and privacy | It changes permissions, tenant boundaries, secrets, personal data, or what one user can observe about another. |
| Data integrity and loss | It deletes, overwrites, migrates, backfills, or transforms durable data, especially without a trivial rollback. |
| Concurrency and retries | Correctness depends on idempotency, ordering, locks, parallel requests, retries, timeouts, or partial failure. |
| External contracts | It changes a public API, event schema, third-party integration, import/export format, or compatibility promise. |
| Lifecycle and architecture | It introduces a long-lived abstraction, persistence model, module boundary, or cross-context dependency that is costly to reverse. |
| Operational blast radius | A mistake could affect many users, corrupt shared state, block recovery, or create an expensive incident. |

Large diffs, many files, or unfamiliar code may increase uncertainty, but they do not automatically require the deep path. Conversely, a one-line authorization change can be high risk.

## Deep-path outputs

For each triggered dimension:

1. State the invariant that must remain true.
2. State the failure or abuse case that would violate it.
3. Decide where the behavior is observable through a public seam.
4. Add one or more rows to the acceptance-and-test matrix.
5. Record a durable decision as an ADR when reversing it later would be expensive or dangerous.

Use `grilling` to surface unresolved decisions and `domain-modeling` to align names, invariants, ownership, and ADRs.

## Acceptance-and-test matrix

Keep the matrix short enough to review. One row represents one independently observable rule.

| Rule or invariant | Observable acceptance criterion | Primary evidence | Test seam |
| --- | --- | --- | --- |
| Example: duplicate command is idempotent | Repeating the same command leaves one durable result and returns the documented status | Integration test with the real persistence boundary | Public command/API plus database transaction |

Choose the evidence that best observes the rule:

- **Domain/unit test:** pure invariant or calculation.
- **API/contract test:** status, payload, validation, or compatibility rule.
- **Persistence integration test:** constraints, transactions, idempotency, concurrency, or materialization.
- **End-to-end test:** user-visible workflow across boundaries.
- **Static analysis:** maintainability, unsafe pattern, or security review point; never the sole proof of behavior.
- **Manual visible check:** presentation or interaction that automation does not yet cover; record exactly what was observed.

## Leaving the deep path

The deepening work is sufficient when:

- every triggered dimension has an explicit invariant;
- material decisions are approved and recorded once;
- each invariant maps to an observable criterion and evidence;
- the implementation can be split into vertical slices without guessing.

If those conditions are not met, continue discovery or use `wayfinder`. Do not hide unresolved decisions inside an implementation plan.
