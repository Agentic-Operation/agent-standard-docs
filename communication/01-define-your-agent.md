# One-pager: Define your agent (Spec-443)

**Audience:** product managers, sponsors, solution architects, compliance/audit.

## What you author

A Spec-443 **profile** — the human-readable contract of one agent. It is the artifact reviewers,
auditors, and integrators read first; the machine artifacts (Spec-444 bootstrap, Spec-445 card) must
join to it on identity and skill keys.

## The sections (all [M] unless noted)

1. Business context & applications — impact areas (lifecycle + operational), stakeholders, drivers.
2. Scope & assumptions — in-scope responsibilities (with eTOM mapping), explicit exclusions with the
   alternative owner, testable assumptions ("Assumed X. If violated: Y").
3. Operational architecture — 8 IG1412 components (Persona, Perception, Knowledge Base, Reasoning,
   Learning, Planning, Action, Communication), sub-function coverage, 4-layer memory, control flow
   (engine + DAG/state machine/HTN + trigger), interface table.
4. Core business capabilities — 3–10 core tasks, each bound to ≥1 skill (`TMF-OASF`/`TMF-GB1033` ID +
   source taxonomy).
5. Data ecosystem — critical inputs (source of record, refresh cadence, quality SLA, SID ref),
   integration touchpoints (protocol + failure mode + Open API ref), infrastructure thresholds.
6. Coordination & multi-agent behavior — posture (Solo/Participates/Orchestrates) + protocol,
   coordination variables (publisher+consumer), conditional sensitivity signals. Spec-443 extension:
   machine-readable topology block for swarms/hierarchies.
7. UX & interaction model — surfaces per actor; discovery & invocation (well-known path, base_url,
   invoke_path, handshake protocol).
8. Security, trust & governance — ODP-EL embargoes/burdens (≥1 each at L3+), NIST AI RMF risk mapping,
   auth scheme, impact radius (constrains autonomy level).
9. ([R]) Performance metrics — operational / learning / business impact, each baseline → target; the
   executive summary's exactly-three outcomes map 1:1 here.
10. ([R]) Deployment — prerequisites (testable pre-deploy), known limitations, deviation register,
    maintenance plan + `autonomyCaseRef` (required L3+).

## Rules of thumb

- Executive summary: one paragraph (150–250 words) + exactly three measurable outcomes.
- Classification must be internally consistent (Agentic AI ⇒ active Learning + Reasoning + Planning
  modules; Non-Agentic ⇒ ≤ L2; High impact radius ≠ L1).
- Companion pointers to the Spec-444 bootstrap and Spec-445 card are required for GA (TBD allowed at draft).

## Next

Author it in `spec/`, instance in `examples/`, validate with `conformance-kit/` (Phase 1), then hand to
onboarding: [agent-bootstrap-management](https://github.com/Agentic-Operation/agent-bootstrap-management).
