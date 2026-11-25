# FAQ — common pitfalls (learned from the TM Forum triad reviews)

1. **Identity mismatch across the triad.** `id` / `uuid` / `version` / `provider` must match
   byte-for-byte across Spec-443, Spec-444, Spec-445. The CI cross-check fails the build on any drift.
2. **Mangled skill IDs.** `TMF-OASF 3015` ≠ `OASF 3015` ≠ `TMF-OASF-3015`. The prefix and the space
   separator are part of the join key; scaffolders must not normalize them.
3. **Empty deontic constraints at L3+.** `deonticConstraints: {embargoes: [], burdens: []}` is
   non-conformant at autonomy L3 or above — declare at least one embargo and one burden (ODP-EL tokens).
4. **Impact radius vs autonomy.** `impactRadius: high` at `L1` is a structural inconsistency; a High
   impact agent with empty constraints is a review blocker.
5. **`target_platform: "local"` committed to version control.** The base bootstrap is environment-agnostic;
   use Spec-444 per-environment `environments[]` override files instead.
6. **One-way companion pointers.** Profile ↔ bootstrap ↔ card references must be bidirectional.
7. **Vague integrations.** "Various internal APIs" or bare "REST" without protocol, failure mode, and
   Open API reference is a recurring review flag.
8. **`skillDiscovery: true` without `discoveryEndpoint`.** The boolean and the endpoint are paired.
9. **Learning module without learning metrics.** If Spec-443 §3.1 declares a Learning Module, §9.2 must
   carry learning metrics and the maintenance plan a drift-assessment cadence.
10. **Marketing-grade executive summary.** Exactly three measurable outcomes, each mapping 1:1 to a
    Spec-443 §9.3 business-impact metric row (baseline → target).
11. **One autonomy level for a whole mesh.** Autonomy is per agent; a swarm/hierarchy has none of its own.
12. **Card `name` used as `id`.** `name` is display text; `id` is the machine registry key.
13. **Secrets embedded in YAML/JSON.** Reference via `*_env` / secrets-manager paths; values resolve at
    deploy time. The pre-commit secret-leak detector will abort the commit.
14. **Stale card after an upgrade.** If `autonomy_level` changed in the profile, the card changed too —
    the cross-check catches it, which is the point.
