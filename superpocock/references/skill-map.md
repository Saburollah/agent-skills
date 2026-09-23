# SuperPocock skill map

This map prevents overlapping skills from issuing contradictory process rules. The phase owner controls the workflow; optional skills add a bounded contribution.

| Situation or phase | Phase owner | Optional Matt/Superpowers contribution |
| --- | --- | --- |
| New feature or behavior change | `brainstorming` | `grilling` and `domain-modeling` only after a high-risk trigger |
| Bug or failing test | `systematic-debugging` | `diagnosing-bugs` for a hard recurring bug or performance regression after reproduction evidence exists |
| Multi-session uncertainty | `wayfinder` | `research` or `prototype` for individual decision tickets |
| Detailed multi-step plan | `writing-plans` | `to-tickets` when the project needs issue-level traceability |
| Implementation loop | `test-driven-development` | Apply the public-seam and test-quality rules summarized by `superpocock`; do not run `tdd` as a second loop authority |
| Plan execution | `executing-plans` | `subagent-driven-development` only when permitted and tasks are independent |
| Checkpoint review | `requesting-code-review` | `receiving-code-review` before acting on reviewer feedback |
| Final review | `code-review` | Keep Spec and Standards findings separate even if reviewed sequentially |
| Completion proof | `verification-before-completion` | Acceptance matrix, static analysis, and visible E2E as applicable |
| Integration choice | `finishing-a-development-branch` | Follow repository-specific PR, issue, and merge rules |

## Conflict rules

1. Direct user instructions and repository instructions win.
2. The phase owner wins over an optional contributor.
3. A specialized skill wins inside its narrow domain, but must return control to the phase owner afterward.
4. Do not invoke both `tdd` and `test-driven-development` as full workflows. SuperPocock uses the latter for execution and carries forward the former's public-seam test-quality principles.
5. Do not invoke both `systematic-debugging` and `diagnosing-bugs` from the start. Begin with systematic debugging; add the Matt diagnostic loop only when the problem remains hard after evidence gathering.
6. Do not create both a Superpowers plan and a second Matt plan containing the same decisions. Keep one plan and link supporting ADRs, issues, and the acceptance matrix.

## Minimum artifact set

### Standard path

- approved design or confirmed ready requirement;
- proportionate plan;
- focused tests and fresh verification evidence;
- review findings when review is available.

### Deep path

Everything from the standard path, plus:

- named risk triggers and invariants;
- acceptance-and-test matrix;
- ADRs for durable decisions;
- traceable issue/spec links when the repository uses an issue tracker;
- integration or end-to-end evidence at each risky boundary.
