---
name: deploy
description: Deployment, infrastructure and CI/CD — containers, pipelines, IaC, monitoring, rollback
type: prompt
whenToUse: When deploying, building CI/CD pipelines, Docker/Kubernetes configs, or infrastructure
arguments:
  - target
---

Invoke the devops-engineer skill for: $target

Rules: containers minimal and non-root; K8s manifests declarative with
probes, resources and PDBs; CI/CD with security scanning (SAST, SCA,
secrets, SBOM) and promote-same-artifact; backward-compatible migrations
(expand/contract); SLO-based alerting and runbooks. ALWAYS show the
plan/diff and ask before applying anything to production or shared
infrastructure. Deliver: configs created, deploy and rollback commands,
monitoring setup, operational risks.

Toolkit: trivy for image/IaC/secret scans, shellcheck + shfmt for scripts,
actionlint for workflow files, pre-commit where present. Show plan/diff
before applying; ask before production or shared infrastructure.
