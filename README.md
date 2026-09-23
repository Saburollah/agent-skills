# SuperPocock skill suite

SuperPocock combines two existing skill collections without replacing either one:

- **Matt Pocock skills:** `matt-v1.0` (`f6de92c`)
- **Obra Superpowers:** `superpowers-v6.3.0` (`a419016`), imported from [obra/superpowers](https://github.com/obra/superpowers) `v6.3.0` at commit `86babb696875227929e85420f287d6309374b93f`

The new `superpocock` skill is the entry point. It uses Superpowers as the default delivery flow and adds Matt-style grilling, domain modeling, ADRs, acceptance matrices, and issue traceability only when a risk check justifies the extra depth.

## Workflow

```text
feature/refactor -> brainstorming ----+
                                     +-> risk check -> plan -> vertical TDD -> review -> evidence -> finish
bug/failure      -> debugging --------+       |
                                             +-> high risk: grilling + domain model + ADR/matrix

large unresolved effort -> wayfinder -> approved decisions -> workflow above
```

High-risk triggers include identity and ownership, authorization, data loss, concurrency and retries, external contracts, long-lived architecture decisions, and large operational blast radius.

## Contents

- All skill directories from `matt-v1.0`
- All skill directories from `superpowers-v6.3.0`
- `superpocock/` with the combined risk-adaptive workflow

The combined skill explicitly resolves overlaps between the two suites. For example, `test-driven-development` owns the execution loop, while Matt's public-seam and test-quality principles are carried into SuperPocock's quality gates.

## Install

Pin projects to a release tag so future updates are deliberate:

```bash
git submodule add --branch superpocock https://github.com/Saburollah/agent-skills.git .agents/skills
git -C .agents/skills checkout superpocock-v1.0.0
```

Then invoke `$superpocock` for non-trivial features, fixes, refactors, migrations, or integrations.

## Sources and licensing

The Superpowers files retain the upstream MIT license in `LICENSES/SUPERPOWERS-MIT.txt`. The Matt skill files are preserved from this repository's `matt-v1.0` tag; no new license terms are asserted for them here.
