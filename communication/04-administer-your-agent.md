# One-pager: Administer your agent (canonical — all three repos)

**Audience:** operators, SRE, GRC, security operations.

## Status lifecycle (identical on all three artifacts)

`draft → in_review → approved → deprecated`. The card's `deploymentStatus` should match the profile and
bootstrap cover-block status.

## Ongoing duties

- **Maintenance plan** (profile §10.4 / card `maintenancePlan`): model-drift assessment cadence (if a
  Learning Module exists), autonomy-certificate renewal (quarterly in the worked example; **required at L3+**
  via `autonomyCaseRef`), periodic security review.
- **Re-validation on any change:** editing any triad artifact or a bound model triggers the 3-stage
  validation (pre-commit → CI cross-check → runtime integrity). A model re-registration/deprecation via
  the Model Management Authority triggers agent re-validation + autonomy re-certification.
- **Per-environment rollout state:** tracked in the Spec-444 deployment/inventory record and the
  Spec-445 `environment-instances` extension — which agent version is live in which environment, health,
  rollout strategy (canary/blue-green/rollback), and per-env `autonomyCaseRef`.
- **Metrics:** watch §9 baselines→targets (operational, learning, business impact); drift beyond tolerance
  feeds the maintenance plan.
- **Deprecation:** set status `deprecated` on all three artifacts, revoke registry discoverability
  (`/.well-known/woa.json`), keep CIDs and transparency-log entries for audit.

## Where each duty lives

| Duty | Artifact | Repo |
|---|---|---|
| Maintenance plan, drift cadence, autonomy case | Spec-443 §10.4 | agent-profile-management |
| Rollout state, per-env overrides, hooks | Spec-444 `environments[]` + inventory record | agent-bootstrap-management |
| Discovery status, env instances, integrity | Spec-445 lifecycle + extensions | agent-discovery-card |
