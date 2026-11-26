# Agentic Operation
## Agentic AI Management Standards: define, onboard, discover, orchestrate, and govern AI agents

AI agents are becoming operational actors in every enterprise, used by internal staff, exposed to
partners and customers, and increasingly invoked by other agents. **Agentic Operation** is the home of
the **Agentic AI Management Standards**: an open, machine-readable standard, plus reference runtime
services, for managing AI agents as first-class, governed members of an organization across their entire
lifecycle.

The ambition: run AI agents **at speed and scale** while the organization always knows **which agents
exist, what they may do, which models and tools they use, where they run, and why they can be trusted**.

## The standard at a glance: one agent, three contracts (the "agent triad")

| Spec | Lifecycle verb | Repository | Medium | Question it answers |
|---|---|---|---|---|
| **Spec-443: AI Agent Profile** | **Define** | [agent-profile-management](https://github.com/Agentic-Operation/agent-profile-management) | Human-readable profile | What is this agent, what may it do, and under which constraints? |
| **Spec-444: AI Agent Bootstrap** | **Onboard** | [agent-bootstrap-management](https://github.com/Agentic-Operation/agent-bootstrap-management) | Declarative YAML (`bootstrap_profile`) | How is it built, tooled, secured, and run? |
| **Spec-445: AI Agent Card** | **Source / discover** | [agent-discovery-card](https://github.com/Agentic-Operation/agent-discovery-card) | JSON, additive over the A2A Agent Card | How do machines discover, verify, and call it? |

**Fourth pillar: model governance.** The [Model Management Authority](https://github.com/Agentic-Operation/model-authority)
governs which models an agent may use. The assignment chain is
**model → skill binding → agent → environment instance**.

The triad succeeds TM Forum **TMF443 / TMF444 / TMF445 v1.0.0** (every extension mapped in each repo's
`spec/annexes/delta-vs-TMF44X.md`) and builds on **IG1412** (L1-L5 autonomy framework, 8-component agent
model), the **A2A Agent Card v1.0**, **Web of Agents (WoA)** discovery at `/.well-known/woa.json`, **MCP**
for tools, **ODP-EL** deontic constraints, **NIST AI RMF** risk mapping, and **Sigstore/Rekor**
transparency-log signing.

## Repository map

**Standards: the normative contracts**

- [agent-profile-management](https://github.com/Agentic-Operation/agent-profile-management) - Spec-443: profile schema, worked examples, conformance kit, publication/validation API and `spec443` CLI
- [agent-bootstrap-management](https://github.com/Agentic-Operation/agent-bootstrap-management) - Spec-444: bootstrap schema, per-environment `environments[]` overrides, scaffold/deploy API and `spec444` CLI
- [agent-discovery-card](https://github.com/Agentic-Operation/agent-discovery-card) - Spec-445: card schema (additive over A2A), Agent Card Registry API, WoA discovery, `spec445` CLI

**Runtime services: reference implementations of the contracts**

- [agent-registry](https://github.com/Agentic-Operation/agent-registry) - production Agent Card Registry: card register/search/versions/verify, environment-instances, WoA at `/.well-known/woa.json` (`:8080`)
- [model-authority](https://github.com/Agentic-Operation/model-authority) - governed model records (id/uuid/version/CID, provenance, eval evidence, license, risk class, approved environments); `resolve` pins `model_ref` → CID; deprecation fires re-certification webhooks (`:8090`)
- [agent-rollout-controller](https://github.com/Agentic-Operation/agent-rollout-controller) - per-environment deploy with override merge, lifecycle hooks, §6.3 inventory record, rollback, card environment-instance sync (`:8091`)
- [tool-mcp-manager](https://github.com/Agentic-Operation/tool-mcp-manager) - registers MCP servers and tool bindings from Spec-444 §3; tracks auth scopes and health (`:8092`)
- [agent-orchestrator](https://github.com/Agentic-Operation/agent-orchestrator) - swarm/hierarchical control plane: Spec-443 §6.4 topology, Spec-444 §4 protocol handlers (a2a_jsonrpc / rep / wo_a / mcp), pub/sub coordination variables, sensitivity signals, per-agent autonomy and outcome metrics (`:8093`)
- [agent-conformance](https://github.com/Agentic-Operation/agent-conformance) - canonical validators, triad cross-check C1-C20, stage-3 runtime integrity check, CI gate templates (`run-all.sh`)

**Documentation**

- [agent-standard-docs](https://github.com/Agentic-Operation/agent-standard-docs) - canonical communication pack / docs site: triad overview, audience one-pagers, model authority, glossary, FAQ, conformance cheat-sheet, worked example, architecture diagrams, references

## The governed agent lifecycle

`define → onboard → source/discover → orchestrate → administer`

- The three artifacts are joined by identity fields (`id`, `uuid`, `version`, `provider`, CID, `integrity_wrapper`) and skill IDs (`TMF-OASF <n>` / `TMF-GB1033 F-xxxx`); cross-check validators C1-C20 enforce the joins in CI.
- Every production-bound artifact passes **three validation stages**: pre-commit (schema + secret-leak scan) → CI gate (schema + cross-check + test suites) → runtime (the `integrity_wrapper` signature is verified against the declared transparency log at startup; failure aborts startup).
- The status lifecycle `draft → in_review → approved → deprecated` is identical on all three artifacts; deprecation revokes registry discoverability while CIDs and transparency-log entries remain for audit.
- Per-environment rollout state lives in the Spec-444 inventory record and the card's `environment-instances`: which agent version is live in which environment, health, and rollout strategy (canary / blue-green / rollback).

## Who this organization is for

- **Chief Business Transformation Officer:** looking to understand the realm of Agentic AI Management Standards and how AI agents can support lifecycle operations in the organization. Start with the [triad overview](https://github.com/Agentic-Operation/agent-standard-docs/blob/main/communication/00-triad-overview.md) and the [audience one-pagers](https://github.com/Agentic-Operation/agent-standard-docs/tree/main/communication) (01 define, 02 onboard, 03 source & discover, 04 administer) in [agent-standard-docs](https://github.com/Agentic-Operation/agent-standard-docs), then the [worked example walkthrough](https://github.com/Agentic-Operation/agent-standard-docs/blob/main/communication/09-worked-example-walkthrough.md).
- **Business Analyst:** looking to leverage internal agent capabilities to extend into external service delivery to customers and partners. Skills carry stable taxonomy IDs in [agent-profile-management](https://github.com/Agentic-Operation/agent-profile-management); cards are published and discoverable through [agent-discovery-card](https://github.com/Agentic-Operation/agent-discovery-card) and the [agent-registry](https://github.com/Agentic-Operation/agent-registry), callable via A2A/MCP, with `environment-instances` describing exactly what is offered in each environment.
- **CTO / CIO / Chief AI Officer:** looking to use AI agents as formal extensions of persons, roles, and people in the enterprise, and to catalog and manage their lifecycle in an assured, controlled way. Define agents with [agent-profile-management](https://github.com/Agentic-Operation/agent-profile-management) (autonomy L1-L5, impact radius, ODP-EL deontic constraints), catalog them in the [agent-registry](https://github.com/Agentic-Operation/agent-registry), keep the per-environment inventory with the [agent-rollout-controller](https://github.com/Agentic-Operation/agent-rollout-controller), govern model bindings through [model-authority](https://github.com/Agentic-Operation/model-authority), and gate everything with [agent-conformance](https://github.com/Agentic-Operation/agent-conformance) plus runtime integrity checks, so the organization knows what it is doing: safe, secure, and governed.
- **Engineers and platform teams:** who have to manage the growing use of AI agents by internal staff, by partners who engage the organization, and by other agents. Stand up the services ([agent-registry](https://github.com/Agentic-Operation/agent-registry), [model-authority](https://github.com/Agentic-Operation/model-authority), [agent-rollout-controller](https://github.com/Agentic-Operation/agent-rollout-controller), [tool-mcp-manager](https://github.com/Agentic-Operation/tool-mcp-manager), [agent-orchestrator](https://github.com/Agentic-Operation/agent-orchestrator)), wire the conformance gates into CI, build catalogs and inventories, and run orchestration and control at scale.
- **AI agents consuming this organization:** every contract here is machine-readable by design. The spec repos publish JSON schemas, OpenAPI APIs, and `spec443` / `spec444` / `spec445` CLIs ([agent-profile-management](https://github.com/Agentic-Operation/agent-profile-management), [agent-bootstrap-management](https://github.com/Agentic-Operation/agent-bootstrap-management), [agent-discovery-card](https://github.com/Agentic-Operation/agent-discovery-card)); the [agent-registry](https://github.com/Agentic-Operation/agent-registry) serves WoA discovery at `/.well-known/woa.json`; [agent-conformance](https://github.com/Agentic-Operation/agent-conformance) provides the validators. This lets agents discover other agents, build their own agent catalogs and inventories, and take part in a well-behaved operational environment that delivers trusted business outcomes at speed and scale.

## Trust, safety, and governance by design

- Every artifact carries the same classification axes: autonomy level **L1-L5** (IG1412), agency class, intelligence class, automation role, mobility, ODA relationship.
- **Impact radius** (low / medium / high) constrains the autonomy level; **ODP-EL deontic constraints** (obligations / prohibitions) are mandatory at L3+.
- **Cryptographic integrity:** a content-addressed `sha256:` CID plus a keyless-signed `integrity_wrapper` (Sigstore/Rekor transparency log), verified at runtime; stage 3 aborts startup on mismatch.
- **Model governance:** `model_ref` resolves through the model authority to a pinned id + version + CID + risk class; model deprecation triggers agent re-validation and autonomy re-certification.
- **Conformance as a gate:** the [agent-conformance](https://github.com/Agentic-Operation/agent-conformance) validators and the C1-C20 cross-check run in every spec repo's `cross-triad` CI job.

## Get started

- 10-minute orientation: [00-triad-overview](https://github.com/Agentic-Operation/agent-standard-docs/blob/main/communication/00-triad-overview.md), then one-pagers [01 define](https://github.com/Agentic-Operation/agent-standard-docs/blob/main/communication/01-define-your-agent.md), [02 onboard](https://github.com/Agentic-Operation/agent-standard-docs/blob/main/communication/02-onboard-your-agent.md), [03 source & discover](https://github.com/Agentic-Operation/agent-standard-docs/blob/main/communication/03-source-and-discover.md), [04 administer](https://github.com/Agentic-Operation/agent-standard-docs/blob/main/communication/04-administer-your-agent.md).
- Author your first agent: quickstarts in each spec repo (`docs/guides/`) and the worked example under `examples/loyalty-agent/`.
- Run the reference stack locally: registry `:8080`, model-authority `:8090`, rollout-controller `:8091`, tool-mcp-manager `:8092`, orchestrator `:8093`.
- Prove conformance end-to-end: `./run-all.sh` in [agent-conformance](https://github.com/Agentic-Operation/agent-conformance).
- Consume as a machine: schemas + OpenAPI contracts + CLIs in the spec repos; discover agents at `/.well-known/woa.json`.

## Contributing

Each repository has its own `CONTRIBUTING.md` (branch convention `vibe/<slug>-…`, draft PRs, conformance-gated CI).
All repositories in this organization are public and licensed **Apache-2.0**.
