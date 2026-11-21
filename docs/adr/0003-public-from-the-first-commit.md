# 0003 – Public from the first commit

- Status: Accepted
- Date: 2026-11-21

## Context

Aegis is a personal project without customer or employer data. Part of its purpose is to be visible: decisions, mistakes and results included. A repository that only becomes public at the end shows a finished state; a public history shows how the project got there.

The main risk of a public infrastructure repository is leaking secrets: Talos machine secrets, kubeconfigs, the Hetzner API token and model API keys.

## Decision

The repository is public from the first commit. Secrets are kept out by three layers:

1. `.gitignore` covers generated Talos configs, kubeconfigs, Terraform/OpenTofu state and `.env` files.
2. Gitleaks runs as a pre-commit hook.
3. Gitleaks runs in CI on every push and pull request.

## Consequences

- Every commit is visible, so commits need to stay clean and reasonably described.
- A leaked secret has to be treated as compromised and rotated; rewriting history is not enough.
