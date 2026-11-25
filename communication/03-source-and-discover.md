# One-pager: Source & discover agents (Spec-445)

**Audience:** procurement, partner ecosystems, registry operators, downstream agents.

## What a card is

A Spec-445 **Agent Card** (JSON, additive over A2A v1.0): identity + integrity, classification,
capabilities (+ `coordination` + skillDiscovery extension), provider, skills with taxonomy joins,
input/output modes + data contracts (SID / OpenAPI — conditional on `oda_relationship`),
authentication + deontic constraints + `impactRadius`, companion refs (bidirectional), lifecycle.

## Discovery & sourcing flow

1. Resolve the agent at its `/.well-known/woa.json` (media type `application/woa+json`) or query the
   registry API (`api/openapi/`).
2. **Verify integrity:** check `integrity_wrapper` signature against the transparency log (Sigstore/Rekor);
   confirm `content_identifier_cid`.
3. **Check fitness:** `classification` (autonomy L1–L5, automation role, mobility, ODA relationship),
   `skills[]` by `TMF-OASF`/`TMF-GB1033` ID + `source_taxonomy` + `bound_core_task`,
   `defaultDataContracts` (TMF Open API refs, SID entities), `authentication.schemes` + scopes.
4. **Check governance:** `deonticConstraints` embargoes/burdens (required non-empty at L3+),
   `impactRadius`, `modelGovernance` (Spec-445 ext: bound models with risk class),
   `environment-instances` (Spec-445 ext: where it runs, health, per-env status).
5. **Invoke:** A2A JSON-RPC 2.0 at `url` + invoke path; MCP for tool-style interactions.

## Red flags (reject or escalate)

- Identity fields that don't match the profile/bootstrap (stale card — cross-check fails).
- `skillDiscovery: true` without `discoveryEndpoint`.
- Empty `deonticConstraints` at L3+; `impactRadius: high` with thin constraints.
- Skills with no `source_taxonomy` or mangled IDs (prefix stripped / dash-separated).
- No `provider` (unauthenticatable in the trust model) or missing `autonomyCaseRef` at L3+.

## Next

Register the card via the registry API; onboard the agent with
[agent-bootstrap-management](https://github.com/Agentic-Operation/agent-bootstrap-management) using its
Spec-444 bootstrap (`tmf444_bootstrap_ref`).
