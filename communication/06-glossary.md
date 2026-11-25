# Glossary

| Term | Meaning | Source |
|---|---|---|
| AI Agent | A system that accepts/adopts a goal and autonomously performs tasks, makes decisions, and interacts with its environment. | IG1412 §4.1 |
| Agentic / Non-Agentic AI | Agentic: proactive, adaptive, self-directed, intentional. Non-Agentic: scripted/static; cannot exceed autonomy L2. | IG1412 §4.1 |
| Autonomy level L1–L5 | L1 Operator, L2 Collaborator, L3 Consultant, L4 Approver, L5 Observer — extent of operation without user involvement. | IG1412 Appendix (authoritative) |
| Agency class / intelligence class / automation role / mobility / ODA relationship | The six classification axes carried on all three artifacts. | Spec-443 Front Matter |
| Skill | Granular, machine-discoverable capability bound to the agent; identified by `TMF-OASF <n>` / `TMF-GB1033 F-xxxx` / `EXTENSION-<id>`. | Spec-443 §4.2 |
| Tool | Stateless external function/resource an agent invokes via MCP or equivalent. Contrast: skills are bound to the agent. | Spec-444 §3 |
| MCP server | Hosts tools/resources for an agent; configured in Spec-444 `mcp_servers` (transports: stdio, sse, websocket, http). | MCP spec |
| CID (`content_identifier_cid`) | Content-addressable `sha256:...` identifier for artifact integrity. Required for production-bound instances. | Triad |
| Integrity wrapper | Keyless signing provenance (`signature_type`, `issuer`, `transparency_log`); verified at runtime (stage 3). | Triad / Sigstore |
| Deontic constraint | Machine-checkable obligation (**burden**) or prohibition (**embargo**) in ODP-EL token vocabulary. ≥1 of each required at L3+. | Spec-443 §8.1 / ODP-EL |
| Impact radius | Low / Medium / High. High = irreversible effects on customers, finances, or regulated disclosures. Constrains autonomy level. | Spec-443 §8.4 |
| Coordination posture | Solo / Participates as member / Orchestrates other agents. | Spec-443 §6.1 |
| Coordination variable | Shared state variable with explicit publisher and consumer (e.g. `DAILY_REDEMPTION_BUDGET`). | Spec-443 §6.2 |
| Sensitivity signal | Conditional behavioral gradient: "If [condition], I will [action]". | Spec-443 §6.3 |
| A2A | Agent-to-agent protocol, commonly JSON-RPC 2.0. Spec-445 is additive over the A2A Agent Card. | A2A / IG1412 §6.2.7 |
| Web of Agents (WoA) | Discovery pattern: agents advertise at `/.well-known/woa.json` (media type `application/woa+json`). | IETF WoA draft |
| Discovery primitive / invocation interface | `well_known_path` + `base_url`/`invoke_path` + `handshake_protocol` (A2A JSON-RPC 2.0, MCP, custom). | Spec-443 §7.2 |
| Cross-check | Mechanical join between triad artifacts (identity fields, skill IDs, tools, auth, lifecycle). Enforced by CI validators. | Annex C / Annex E |
| Conformance classes | [M] mandatory, [R] recommended, [O] optional, [M-conditional] mandatory-when-condition. | Spec-44X conformance clause |
| Lifecycle hooks | Executable scripts at `pre_bootstrap` / `post_bootstrap` / `pre_deploy` (signing, autonomy-case generation). | Spec-444 §8 |
| MUI | Minimum User Involvement — autonomy scored by frequency of required human intervention. | IG1412 §6.2.9 |
| Model Management Authority | Governed registry of models (identity, provenance, eval evidence, license, risk class, policy) that skill `model_ref`s resolve through. | Spec-444 annex |
