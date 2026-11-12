---
name: security
description: Security audit and remediation — threat modeling, OWASP, dependency and secret scanning
type: prompt
whenToUse: When the user asks for a security audit, threat model, or remediation of vulnerabilities
arguments:
  - target
---

Invoke the security-engineer skill and audit: $target

If no target given, audit the current working tree / recent changes.
Map the attack surface, STRIDE the trust boundaries, check the OWASP Top
10/API categories in code, run the project's dependency and secret scanning
tooling, and review new dependencies' advisories. Deliver findings ranked
critical/high/medium/low with file:line evidence and concrete remediation.
Remediate when asked; ask before changes with wide blast radius. Preserve
security evidence verbatim.

Tool workflow: semgrep for code SAST (targeted rules first), trivy for
dependency/container/IaC/secret scanning, shellcheck for shell scripts,
actionlint for CI workflows. Never expose secrets in output; never suppress
findings; record results in the task handoff VALIDATION.md.
