# GitOps Platform — Kubernetes Infrastructure

> A Kubernetes platform a small team can actually operate.

## What I Built

A full GitOps delivery platform for a distributed team shipping web apps and AI agents. The goal: developers deploy by opening a PR, and access, secrets, and rollbacks all follow the same path.

### Infrastructure

- **Cluster**: DigitalOcean Kubernetes (DOKS) provisioned with OpenTofu
- **Delivery**: Helm charts deployed through ArgoCD — PR-driven GitOps workflow
- **Secrets**: Infisical for secret injection, scoped per environment
- **Observability**: Prometheus + Grafana + Loki stack — failures show up on a dashboard before Slack

### How It Works

```
Developer opens PR
       │
       ▼
GitHub Actions ── lint/test/build ──► Container image → Harbor registry
       │
       ▼
ArgoCD detects change in Helm values
       │
       ▼
Syncs to DOKS cluster
       │
       ├── Prometheus scrapes metrics
       ├── Loki aggregates logs
       └── Grafana dashboards + alerts
```

## Decisions

| Decision | Why |
|---|---|
| ArgoCD over Flux | Team already understood the UI; Flux's GitOps Toolkit added complexity we didn't need |
| Infisical over Vault | Faster onboarding for a small team; OpenBao migration planned for later |
| Helm over raw manifests | Templating for per-environment values; ArgoCD syncs Helm natively |
| Loki over ELK | Lightweight, integrates with Grafana, no separate Elasticsearch cluster to manage |

## Outcome

The team deploys by opening a PR. Access, secrets, and rollbacks follow the same path.

## Stack

`OpenTofu` · `Helm` · `ArgoCD` · `Infisical` · `Prometheus` · `Grafana` · `Loki` · `DOKS`

## Context

Built as Platform Engineer at [WeOwn](https://weown.net) (2025–present). Source code is proprietary.
