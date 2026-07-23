# field-engineering-otel

GitOps knobs for the Astronomy Shop (`otel-demo` namespace on field-engineering EKS).

Same org pattern as `field-engineering` (Terraform), `field-engineering-cdk`, and `field-engineering-cfn` —
this repo is the **clean PR target** for Aiden SRE → infrastructure-engineer remediations.

## Exact paths (for IE / mcp-github)

| Knob | Path |
|------|------|
| Healthy flagd | `overlays/baseline/demo.flagd.json` |
| flagd ConfigMap | `overlays/baseline/flagd-config.yaml` |
| Healthy resource limits | `overlays/baseline/resources.yaml` |
| O1 fault flagd | `overlays/o1-bad-catalog/` |
| O2 schema restore Job | `overlays/o2-schema-fix/job.yaml` |
| O3 low memory | `overlays/o3-memory-pressure/resources.yaml` |

Argo Application `otel-demo-knobs` syncs `overlays/baseline` → ns `otel-demo`.

Operator inject/reset scripts live in `Infra-Provisioning` (`otel-sre-demo/scripts/`), not here —
keep this repo uncluttered for demo PRs.

## After merge

Argo auto-syncs baseline, or:

```bash
# from Infra-Provisioning
OTEL_SRE_GITOPS_DIR=/path/to/field-engineering-otel \
  otel-sre-demo/scripts/sync-overlay.sh baseline
```
