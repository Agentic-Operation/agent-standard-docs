# Agent Standard — published documentation (Spec-443 / Spec-444 / Spec-445)

This repo is the **canonical home of the communication package** for the agent triad. The spec repos
link here instead of keeping their own copies.

## Spec repos (contracts are canonical there)

| Spec | Repo | Verb |
|---|---|---|
| Spec-443 AI Agent Profile | [agent-profile-management](https://github.com/Agentic-Operation/agent-profile-management) | Define |
| Spec-444 AI Agent Bootstrap | [agent-bootstrap-management](https://github.com/Agentic-Operation/agent-bootstrap-management) | Onboard |
| Spec-445 AI Agent Card | [agent-discovery-card](https://github.com/Agentic-Operation/agent-discovery-card) | Source |

## Runtime service repos (implement the specs)

| Service | Repo | Implements |
|---|---|---|
| Agent Card Registry | [Agent-Registry](https://github.com/Agentic-Operation/Agent-Registry) | Spec-445 registry API (`api/openapi/registry-api.yaml` in agent-discovery-card) |
| Model Management Authority | [model-authority](https://github.com/Agentic-Operation/model-authority) | Spec-444 §2.2 `model_bindings` + `spec/annexes/model-authority-record.schema.json` in agent-bootstrap-management |
| Rollout controller | [agent-rollout-controller](https://github.com/Agentic-Operation/agent-rollout-controller) | Spec-444 §6.2 `environments[]`, §6.3 inventory, §8 hooks; bootstrap API |
| Orchestrator (swarm/hierarchy) | [agent-orchestrator](https://github.com/Agentic-Operation/agent-orchestrator) | Spec-443 §6.4 topology, Spec-444 §4 protocol handlers, Spec-445 `coordination` |
| Tool & MCP manager | [tool-mcp-manager](https://github.com/Agentic-Operation/tool-mcp-manager) | Spec-444 §3 `tool_bindings` / `mcp_servers` |
| Conformance kit | [agent-conformance](https://github.com/Agentic-Operation/agent-conformance) | validators, cross-check (C1–C20), stage-3 runtime check, CI templates |

## Pack contents

- [communication/00-triad-overview.md](communication/00-triad-overview.md) — the triad, join keys, validation stages
- [communication/01..04](communication/) — audience one-pagers: define / onboard / source / administer
- [communication/05-model-management-authority.md](communication/05-model-management-authority.md) — model → skill → agent → environment
- [communication/06-glossary.md](communication/06-glossary.md) · [07-faq.md](communication/07-faq.md) · [08-conformance-cheat-sheet.md](communication/08-conformance-cheat-sheet.md) · [09-worked-example-walkthrough.md](communication/09-worked-example-walkthrough.md)
- [architecture/](architecture/) — mermaid triad + lifecycle diagrams
- [references/REFERENCES.md](references/REFERENCES.md) — related sources + authority precedence
- [services/](services/) — runtime service layer notes
