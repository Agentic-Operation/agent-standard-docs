# One-pager: Onboard your agent (Spec-444)

**Audience:** platform engineers, DevOps, agent developers.

## What you author

A Spec-444 **bootstrap specification** — declarative YAML under `bootstrap_profile` that a scaffolder
turns into a runnable agent (repo + tests + Dockerfile + CI), then signs and deploys per environment.

## Anatomy of the YAML

- `generation` — `target_framework` (open-agent-spec / wayflow / langgraph / crewai / autogen / custom;
  must match the profile's §3.4 `execution_engine`), version constraint, language, output structure,
  tests, Dockerfile, CI template, license header.
- `skill_bindings` — every profile §4.2 skill row bound to an implementation (`skill_id` string-equality
  join; adapter: huggingface_pipeline / mlflow_model / langgraph_subgraph / wayflow_node / python_function;
  `model_ref` resolved via the **Model Management Authority** to a pinned, signed model; fallback behavior).
- `tool_bindings` + `mcp_servers` — external tools as MCP tools/resources (or rest_api/function), MCP
  server transports (stdio/sse/websocket/http), `env_secrets` (names only — values from the secrets
  manager), health checks. Each binding corresponds to a profile §5.2 touchpoint.
- `protocol_handlers` — a2a_jsonrpc / rep / mcp / wo_a / custom, joined to the profile §6.1 posture.
- `security_config` — auth provider (oauth2_oidc / keycloak / mtls / api_key), token validation, scopes,
  secrets backend + kv_path, Sigstore signing (`sign_artifacts`).
- `deployment` — platform, resource constraints, scaling (min_replicas 0 for L4+, ≥1 below to keep
  surfaces warm), observability (json logs, prometheus/otel). **Spec-444 extension:** `environments[]`
  per-env overrides (platform, endpoints, kv_path, flags) + the **deployment/inventory record**.
- `validation` + `testing` — schema URI, strict mode, pre-commit hooks (incl. secret-leak detector),
  failure policy `fail_commit` for production; acceptance criteria joined to profile §9 metrics.
- `lifecycle_hooks` — `pre_bootstrap` (secret-resolution check), `post_bootstrap` (autonomy-case
  generator — required at L3+), `pre_deploy` (artifact signing — required for production).

## Hard rules

- Never embed secret values — reference `*_env` / kv paths; values resolve at deploy time.
- Base YAML is environment-agnostic: no `target_platform: "local"` in version control; use
  `environments[]` overrides.
- Every `skill_id` in the bootstrap must exist in the profile §4.2 (and vice versa, or a deviation is
  registered). The TMF prefix is part of the ID.

## Next

Validate with `conformance-kit/`, scaffold with `tools/cli` (`spec444 scaffold`), deploy per environment
(`spec444 deploy --env prod`), and publish the resulting Spec-445 card for discovery:
[agent-discovery-card](https://github.com/Agentic-Operation/agent-discovery-card).
