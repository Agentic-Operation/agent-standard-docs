# Conformance cheat sheet

## Classes

| Marker | Class | Violation meaning |
|---|---|---|
| [M] | MANDATORY | Section/field absent or placeholder → **non-conformant** |
| [R] | RECOMMENDED | Absent/deviating without written justification in the Deviation Register → conformant but flagged |
| [O] | OPTIONAL | Present (conformant content) or absent; no justification needed |
| [M-conditional] | MANDATORY (conditional) | Required when the named condition holds (e.g. `defaultDataContracts` when `oda_relationship ≠ Standalone`; `autonomyCaseRef` at L3+) |

Two levels apply everywhere: the **section presence** class on the section header, and the
**field-level** class in each section's Field Conformance table. Conformance = section present AND every
[M] field populated AND every [M-conditional] field populated when its condition holds AND cross-check
joins pass.

## Three-stage validation (production-bound instances must have all three)

| Stage | Trigger | Checks | Failure |
|---|---|---|---|
| 1 Pre-commit | `git commit` | schema validator, secret-leak detector | aborts commit |
| 2 CI gate | every PR | schema + cross-check validator + unit/integration/acceptance tests | blocks merge |
| 3 Runtime | agent startup | `integrity_wrapper` signature vs transparency log | aborts startup |

## Deviation register

Every absent/altered [R] section and every non-conformant [O] addition must be recorded
(section, deviation, justification, approver, date). An empty register claims full conformance —
unusual at draft stage; expect review.

## Self-check

Run `spec/annexes/self-check.md` before submitting an instance for review; the conformance-kit
validators automate most of it.
