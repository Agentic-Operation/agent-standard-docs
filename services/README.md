# Runtime services layer

The triad specs (Spec-443/444/445) are contracts; the services below run them. All live in this org:

- **Agent-Registry** — card registry + WoA discovery + integrity verification + environment instances.
- **model-authority** — governed model records; `resolve` pins `model_ref` → id+version+CID; deprecation fires re-certification webhooks (C19).
- **agent-rollout-controller** — scaffold/deploy per environment (`environments[]` overrides), lifecycle hooks, §6.3 inventory, rollback; syncs card environment instances to the registry.
- **agent-orchestrator** — swarm/hierarchical control plane: loads Spec-443 §6.4 topology, wires Spec-444 §4 protocol handlers (a2a_jsonrpc/rep/wo_a/mcp), pub/sub coordination variables, sensitivity signals, per-agent autonomy + outcome tracking (individual or mesh-level outcomes).
- **tool-mcp-manager** — registers and health-checks MCP servers and tool bindings from Spec-444 §3, exposes them to agents.
- **agent-conformance** — canonical validators + triad cross-check (C1–C20) + stage-3 runtime integrity check + CI templates; spec repos run these in their `cross-triad` CI job.

Data flow: profile (define) → bootstrap (onboard: scaffold via rollout-controller, models via
model-authority, tools via tool-mcp-manager) → card registered in Agent-Registry (source/discover) →
orchestrator composes agents into swarms/hierarchies → administer via per-environment inventory +
registry environment instances.
