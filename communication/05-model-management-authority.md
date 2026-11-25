# Model Management Authority — the fourth pillar

The triad references models through `model_ref` / `model_uri` in skill bindings and through learning
metrics and drift cadences. Without a governed model layer, onboarding can bind an unvetted model and
an autonomy certificate has no model lineage to stand on. The **Model Management Authority** is therefore
designed in tandem with Spec-443/444/445, not after them.

## Authority record (per model)

The normative record schema lives in the Spec-444 annex
(`agent-bootstrap-management/spec/annexes/`). Each record carries:

- **Identity & integrity:** model `id`, `uuid`, `version`, `content_identifier_cid` (sha256), signature / transparency log.
- **Provenance:** training data, pipeline, base model lineage.
- **Evidence:** evaluation results against named benchmarks **with versions**.
- **Policy:** license, risk class, allowed-use policy, deontic tokens (ODP-EL), approved environments.

## Structured assignment chain

```text
Model (authority record)
   │  resolved to a pinned, signed version
   ▼
Spec-444 model_bindings / skill_bindings[*].implementation.model_ref   (e.g. models:/ChurnScorer/Production)
   │  string-equality join on model id + version + CID
   ▼
Agent identity (id / uuid / version / provider — identical across Spec-443 / Spec-444 / Spec-445)
   │  per-environment binding
   ▼
Environment instance (Spec-445 environment-instances extension; Spec-444 deployment/inventory record)
```

## Governance rules

- **Model risk class × agent `impactRadius` × `autonomy_level` are jointly constrained.** A high-risk
  model bound into a high-impact-radius, L4/L5 agent is a structural inconsistency — mirroring the
  existing rule that `impact_radius: High` at `L1` is non-conformant.
- **Re-certification triggers:** re-registration, re-training, or deprecation of a bound model triggers
  agent re-validation (CI cross-check) and autonomy-certificate renewal (required at L3+, via the
  `autonomyCaseRef` lifecycle hook).
- Secrets and model credentials are injected at deploy time through the secrets manager
  (Spec-444 `security_config`) — never embedded in YAML/JSON artifacts.
