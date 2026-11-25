# The Agent Triad — Spec-443 / Spec-444 / Spec-445

One AI agent, three contracts. This organization hosts three specifications that together let an
organization **define, source, onboard, and administer** AI agents:

| Spec | Repository | Lifecycle verb | Medium | Question it answers |
|---|---|---|---|---|
| **Spec-443 — AI Agent Profile** | [`agent-profile-management`](https://github.com/Agentic-Operation/agent-profile-management) | **Define** | Human-readable narrative (Markdown/Word) | What is this agent, what may it do, under what constraints? |
| **Spec-444 — AI Agent Bootstrap** | [`agent-bootstrap-management`](https://github.com/Agentic-Operation/agent-bootstrap-management) | **Onboard** | Declarative YAML under a `bootstrap_profile` root key | How is it built, tooled, secured, and run? |
| **Spec-445 — AI Agent Card** | [`agent-discovery-card`](https://github.com/Agentic-Operation/agent-discovery-card) | **Source** | JSON, additive extension of the A2A Agent Card | How do machines discover, verify, and call it? |

**Fourth pillar — the Model Management Authority** (see [05-model-management-authority.md](05-model-management-authority.md))
governs which models an agent may use. Assignment chain: **model → skill binding → agent → environment instance**.

## Relationship to TM Forum

Spec-443 / Spec-444 / Spec-445 are successors of TM Forum **TMF443 / TMF444 / TMF445 v1.0.0** (alpha).
Each `Spec-44X` = `TMF44X` + extensions; every extension is mapped to the TM Forum original in
`spec/annexes/delta-vs-TMF44X.md`. Authority precedence is preserved from the originals:
**IG1412** prevails for the L1–L5 autonomy framework and the 8-component agent model;
**A2A** prevails for base Agent Card fields; each `Spec-44X` prevails for its own extensions.

## The join keys that hold the triad together

- **Identity fields** identical across all three artifacts: `id`, `uuid`, `version`, `provider`,
  plus production-bound `content_identifier_cid` (`sha256:...`) and `integrity_wrapper`
  (keyless signing: `signature_type`, `issuer`, `transparency_log`, e.g. Sigstore/Rekor).
- **Skill IDs** are string-equality join keys: `TMF-OASF <number>` / `TMF-GB1033 F-xxxx`.
  The TMF prefix is part of the identifier — never stripped or re-separated. New skills: `EXTENSION-<proposed-id>`.
- **Companion pointers are bidirectional** (profile ↔ bootstrap ↔ card). A one-way pointer is non-conformant.
- The **cross-check validators** in each repo's `conformance-kit/` enforce these joins in CI.

## Classification snapshot (carried on all three artifacts)

`autonomy_level` L1–L5 (L1 Operator, L2 Collaborator, L3 Consultant, L4 Approver, L5 Observer — IG1412);
`agency_class` Agentic AI / Non-Agentic AI (Non-Agentic cannot exceed L2); `intelligence_class`
(Simple Reflex … Utility-Based Learning); `automation_role` Worker / Planner / Orchestrator Agent;
`mobility` Static / Single-Environment / Cross-Environment; `oda_relationship` Standalone /
Agentified ODA Component / ODA-Adjacent (drives the conditional data contracts on the card).

## Three-stage validation (every production-bound artifact)

1. **Pre-commit** — schema validator + secret-leak detector; failure aborts the commit.
2. **CI gate** — schema validator + cross-check validator + test suites; failure blocks merge.
3. **Runtime** — verify the `integrity_wrapper` signature against the declared transparency log at agent startup; failure aborts startup.

## Lifecycle verbs → repositories

- **Define → Spec-443 (profile):** classification, scope & assumptions, operational architecture
  (8 IG1412 components, 4-layer memory hierarchy, control flow, interface table), core tasks ↔ skills,
  data ecosystem, coordination & multi-agent behavior, UX & discovery/invocation, security & governance
  (ODP-EL deontic constraints, NIST AI RMF risk mapping, impact radius), performance metrics, deployment.
- **Source → Spec-445 (card) + registry:** discovery at `/.well-known/woa.json`, skill search by
  taxonomy ID, Sigstore integrity verification, sourcing checklist.
- **Onboard → Spec-444 (bootstrap):** runtime targeting, skill bindings to code/models, tool & MCP
  bindings, protocol handlers, security/secrets injection, deployment & observability, validation,
  lifecycle hooks. Spec-444 extensions add per-environment `environments[]` overrides, `model_bindings`,
  and the per-environment deployment/inventory record.
- **Administer → all three:** status lifecycle (draft / in_review / approved / deprecated), maintenance
  plan, model-drift cadence, autonomy-certificate renewal (required at L3+), re-validation on any change,
  per-environment rollout state.

## Multi-agent systems

Coordination posture is one of **Solo / Participates / Orchestrates** ("Orchestrates" requires
`automation_role = Orchestrator Agent`). Coordination protocols: A2A JSON-RPC 2.0, REP, WoA, MCP.
Coordination variables have an explicit publisher and consumer; sensitivity signals are conditional
("If X, then I will Y"). Spec-443 adds a machine-readable **topology block** for swarms/hierarchies;
Spec-445 carries it in the `coordination` object. Note: a mesh has no single autonomy level — each
agent in it keeps its own L1–L5.
