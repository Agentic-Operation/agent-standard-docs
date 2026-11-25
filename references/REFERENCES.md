# References — related sources and authority precedence

Canonical copy: `agent-profile-management`. Mirrored in `agent-bootstrap-management` and
`agent-discovery-card`.

## TM Forum (originals and frameworks)

| Source | Used for | Authority note |
|---|---|---|
| TMF443 AI Agent Profile Template v1.0.0 | Base of Spec-443 | Spec-443 prevails for its extensions; delta in `spec/annexes/delta-vs-TMF44X.md` |
| TMF444 AI Agent Bootstrap Specification v1.0.0 | Base of Spec-444 | same |
| TMF445 AI Agent Card Specification v1.0.0 | Base of Spec-445 | A2A prevails for base card fields; Spec-445 for extensions |
| IG1412 AI Agent Specification | L1–L5 autonomy framework, 8 canonical components, sub-functions, memory hierarchy | **Authoritative** where triad docs differ |
| GB921 eTOM | L2/L3 process mapping (`etom_process_ref`) | TM Forum |
| GB922 SID | Data entities in `defaultDataContracts` | TM Forum |
| GB988 | Metrics definitions (§9) | TM Forum |
| GB1022 ODA | Business capabilities / ODA Components (`oda_relationship`, `bound_business_capability`) | TM Forum |
| GB1033 Functional Framework | `TMF-GB1033 F-xxxx` skill IDs | TM Forum |
| TM Forum Open APIs (TMF6xx, e.g. TMF629, TMF637, TMF678) | Integration touchpoints, data contracts | cite name + version |

## External standards

| Source | Used for | Authority note |
|---|---|---|
| A2A Protocol (Agent Card v1.0, JSON-RPC 2.0) | Base of Spec-445 card; handshake | **Authoritative** for A2A base fields; every A2A card is a valid Spec-445 card |
| IETF Web of Agents / HAIDIP draft | `/.well-known/woa.json` discovery, envelope | IETF |
| Model Context Protocol (MCP) | Tools/resources, `mcp_servers` config | MCP spec |
| OASF / Agntcy skill taxonomy | `TMF-OASF <n>` skill IDs | underlying catalogue for the TMF prefix |
| Sigstore / Rekor | `integrity_wrapper`, signing lifecycle hooks | CNCF |
| NIST AI RMF (adversarial ML, AAI001–006, AI 100-1/100-3) | Risk mapping | NIST |
| ODP-EL | Deontic embargoes/burdens token vocabulary | ODP |
| JSON Schema draft-07 / OpenAPI 3.x | Normative schemas in `schemas/`, APIs in `api/openapi/` | IETF / OAI |

## Precedence rule (from the triad)

Where documents differ: **IG1412** for autonomy framework and agent components; **A2A** for base card
fields; the owning **Spec-44X** for its extensions; **TM Forum** originals otherwise.
