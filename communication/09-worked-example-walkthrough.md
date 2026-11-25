# Worked example — Loyalty Management Agent

The same agent instance appears in all three repos' `examples/loyalty-agent/` so the join keys can be
verified side by side (this mirrors the TM Forum annexes).

- **Classification:** `autonomy_level: L3` (Consultant), `agency_class: Agentic AI`,
  `intelligence_class: Utility-Based Learning`, `automation_role: Worker Agent`,
  `mobility: Cross-Environment`, `oda_relationship: ODA-Adjacent`.
- **Identity (must match in all three artifacts):** `id: loyalty-management-agent-v1(-bootstrap|-card)`,
  `uuid: 9e3b2f5d-4a8c-4f6e-8b1d-7c9a2e5f3b6d`, `version: 1.0.0-stable`,
  `provider: <team>`, CID `sha256:...`, Sigstore `integrity_wrapper`.
- **Skills (7):** `TMF-OASF 3015`, `3016`, `3020`, `3021`, `2046`, `2051`, `TMF-GB1033 F-1842` — each bound
  to exactly one core task, each with `source_taxonomy`, and each present in Spec-443 §4.2,
  Spec-444 `skill_bindings`, and Spec-445 `skills[]`.
- **Tools / integrations:** POS & e-commerce, Marketing Execution (ESP), CRM — bound as
  Spec-444 `tool_bindings` (MCP tools/resources) and advertised as Spec-445 `defaultDataContracts`
  (TMF629 v4, TMF678 v4, SID entities).
- **Coordination:** posture "Participates as a member of a multi-agent system", protocol
  `a2a_jsonrpc`, variables `DAILY_REDEMPTION_BUDGET`, `MEMBER_CONSENT_FLAG` (each with publisher +
  consumer), conditional sensitivity signals.
- **Security:** `oauth2_oidc` (Keycloak), scopes `agent:execute, pos:write, ads:write, crm:read`;
  ODP-EL embargoes (`auto_finalize_payment(ALL_AI)` …) and burdens (`provide_attribution_explanation(...)` …);
  `impactRadius: medium`.
- **Lifecycle:** `deploymentStatus: approved`, ISO-8601 `lastUpdated`, maintenance plan (monthly drift
  assessment, quarterly autonomy-certificate renewal), `autonomyCaseRef` (required at L3+).

Walkthrough: start at the profile (`agent-profile-management/examples/loyalty-agent/`), follow
`tmf444_bootstrap_ref` to the bootstrap, then `tmf445_agent_card_ref` to the card — and back. If any
join key differs, the conformance-kit validator fails.
