# Aegis

**An autonomous SRE agent for Kubernetes, built eval-first.**

Aegis watches a self-hosted Kubernetes cluster, diagnoses incidents and proposes fixes. It never applies a fix on its own: every write action requires human approval. The core of the project is not the agent but the evaluation pipeline that measures how good the agent actually is.

> Status: **Phase 0 – Infrastructure.** Nothing runs yet. This repository is built in public, decisions included.

## Why

Most agent projects stop at the demo. Aegis is built around the question that comes after the demo: *how do you know it works, and how do you know it still works after the next prompt or model change?* Every agent run is traced, every change is evaluated against a fixed set of reproducible incidents, and the results are versioned.

## Target architecture

1. **Signal source** – Prometheus and Alertmanager on a self-hosted Talos Linux cluster send alerts to the agent via webhook.
2. **Agent** – a single LangGraph agent (Claude as the default model) triages the alert, gathers context (pod logs, events, metrics) with read-only tools and produces a root-cause diagnosis and a proposed remediation.
3. **Human in the loop** – remediations are approval requests, never autonomous actions.
4. **Observability** – every agent step is traced with OpenTelemetry and exported to a self-hosted Langfuse instance: latency, tokens and cost per incident.
5. **Evaluation** – a framework-independent harness runs the agent against reproducible chaos scenarios with known ground truth and reports accuracy, hallucination rate, latency and cost.

## Scope

The project is deliberately cut to what fits next to university:

| Phase | Content |
|---|---|
| 0 – Infrastructure | Hetzner Cloud, Talos Linux cluster, Prometheus/Grafana |
| 1 – Foundation | 10 reproducible chaos scenarios, single agent with read-only tools, Langfuse tracing |
| 2 – Eval-first | 20 scenarios with ground truth, eval harness, baseline metrics, evals in CI |
| 5 – Visibility | Architecture diagram and published eval results in this README |

Multi-agent orchestration and production hardening are out of scope for now. A model comparison is the first candidate if time allows.

## Success criteria

- Root-cause accuracy above 80 % on the scenario set
- Every agent run fully traced, with cost attribution
- At least one documented case where the evals caught a regression before merge
- Reproducible setup and published benchmark numbers

## Repository layout

| Path | Content |
|---|---|
| `infra/` | Hetzner and Talos provisioning |
| `cluster/` | Manifests and Helm values for monitoring and Langfuse |
| `scenarios/` | Chaos scenarios: injection, ground truth, cleanup |
| `agent/` | The LangGraph agent |
| `evals/` | Eval harness and versioned results |
| `docs/adr/` | Architecture decision records |

## Development

Requirements: Linux (or WSL2), [uv](https://docs.astral.sh/uv/), git.

```bash
uv sync
uv run pre-commit install
```

Secrets never go into this repository. Gitleaks runs as a pre-commit hook and in CI on every push.
