---
name: superpocock
description: Use for non-trivial feature work, bug fixes, refactors, migrations, or integrations that need a risk-adaptive workflow combining Superpowers delivery discipline with Matt Pocock's deeper decision, domain, and traceability practices.
---

# SuperPocock

Take work from an understood problem to evidence-backed completion without applying every process to every task. Use Superpowers as the default delivery spine. Add Matt-style depth only where risk justifies it.

## Non-negotiable rules

1. Read repository instructions before acting: `AGENTS.md`, `CLAUDE.md`, domain docs, ADRs, and the originating issue or spec when present.
2. User instructions and repository rules outrank this workflow.
3. Gather facts from the environment yourself. Ask the user only for decisions, preferences, missing authority, or information unavailable to the agent.
4. Do not stack overlapping skills as competing authorities. Follow the phase owner named below.
5. Do not claim completion without fresh verification evidence.

## Route the work

Choose the entry path before implementation:

- **Feature, behavior change, or refactor:** invoke `brainstorming` and obtain design approval.
- **Bug, failing test, or unexpected behavior:** invoke `systematic-debugging` before proposing a fix. Reproduce the problem and identify the cause.
- **Large effort with unresolved decisions that exceeds one session:** invoke `wayfinder` before detailed design or planning.
- **Ready specification or issue with no meaningful design uncertainty:** skip discovery already completed, but still run the risk check.

Read [skill-map.md](references/skill-map.md) when choosing between overlapping or optional skills.

## Run the risk check

Before writing an implementation plan, evaluate the change against [risk-check.md](references/risk-check.md).

- **Standard path:** no high-risk dimension. Continue with the approved design and a proportionate plan.
- **Deep path:** at least one high-risk dimension. Record which dimension triggered it, then invoke `grilling` and `domain-modeling` to expose invariants and durable decisions. Create the acceptance-and-test matrix defined in the reference.
- **Wayfinding path:** the destination is understood but the decisions cannot fit in one session. Use `wayfinder`; do not pretend a detailed implementation plan is already possible.

Do not treat file count, diff size, or task duration alone as high risk. Risk is about consequences and uncertainty.

## Plan the change

For multi-step work, invoke `writing-plans`. The plan must connect each requirement to a vertical implementation slice and its evidence.

On the deep path, also:

- record an ADR when a decision is durable or expensive to reverse;
- use `to-tickets` only when the project uses an issue tracker and the work benefits from independently traceable slices;
- make identity, authorization, lifecycle, failure, concurrency, and rollback rules explicit when relevant;
- link the approved design, ADRs, issues, and acceptance matrix instead of copying the same decision into several places.

For a small, ready change, a short inline plan is enough. Do not manufacture documents that will not help implementation or review.

## Implement in vertical TDD slices

Use `test-driven-development` as the phase owner for the red-green-refactor loop:

1. Select one observable behavior at a public seam.
2. Name the production change that would make the test fail.
3. Write the smallest test for that behavior and watch it fail for the expected reason.
4. Add the minimum implementation and watch the test pass.
5. Refactor only while the tests remain green.
6. Repeat for the next acceptance rule.

Apply these Matt-style test-quality constraints throughout:

- test behavior through public interfaces, not private implementation;
- use an independent expected result rather than recomputing the production logic;
- prefer real collaborators and integration tests at risky persistence or concurrency seams;
- keep one primary rule per test so failures remain diagnostic;
- agree the important seams before investing in a large test set.

Use `executing-plans` for sequential execution. Use `subagent-driven-development` or `dispatching-parallel-agents` only when the environment supports it, the tasks are genuinely independent, and the user or governing instructions permit delegation.

## Review and prove the result

Review at two levels:

1. Use `requesting-code-review` at meaningful implementation checkpoints when a reviewer is available.
2. Before integration, use `code-review` against a fixed point for both specification fidelity and repository standards. If subagents are unavailable, perform the two axes sequentially and keep their findings separate.

Then invoke `verification-before-completion` and collect fresh evidence proportionate to the change:

- focused tests for each changed behavior;
- the broader relevant test suite;
- build, type checking, and linting when configured;
- static analysis when configured, interpreted relative to scope and baseline;
- a visible end-to-end check for user-facing behavior;
- explicit confirmation that every acceptance-matrix row has evidence.

A passing quality gate, high test count, or successful build is one signal, not proof of correctness by itself.

## Finish

Invoke `finishing-a-development-branch` only after the verification evidence is fresh and review findings are resolved or consciously accepted. Report:

- what changed;
- which risk path was used and why;
- what evidence was run and its result;
- any residual risk or deferred decision;
- the exact integration options available to the user.
