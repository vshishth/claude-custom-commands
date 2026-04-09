---
description: Security audit identifying vulnerabilities with severity and fixes
argument-hint: file path, directory, or paste code
allowed-tools: Read, Grep, Glob, Bash(npm audit:*, pip audit:*, bundle audit:*, cargo audit:*, go mod:*, trivy:*, semgrep:*)
---

# Security Audit

Act as a Principal Engineer with security expertise. Perform a thorough security audit.

```
$ARGUMENTS
```

## Audit Scope

Check systematically against each category:

1. **Input validation** — Injection (SQL, NoSQL, command, XSS), path traversal, deserialization, template injection
2. **Authentication & authorization** — Auth bypass, privilege escalation, missing checks, session management, token handling
3. **Data protection** — Secrets in code, PII exposure, missing encryption, insecure storage, logging of sensitive data
4. **Dependencies** — Known CVEs (run `npm audit` / `pip audit` / equivalent), outdated packages, supply chain risks
5. **Configuration** — Permissive CORS, debug mode in prod, insecure defaults, exposed endpoints, missing security headers
6. **Cryptography** — Weak algorithms, improper key management, predictable tokens, hardcoded keys
7. **OWASP Top 10** — Explicitly verify each category; note which are not applicable to this codebase

## Output

For each vulnerability found:
- **Severity**: Critical / High / Medium / Low (use CVSS reasoning)
- **Location**: file:line
- **CWE**: Reference number
- **Issue**: What's wrong and how it could be exploited
- **Fix**: Specific code change to remediate — not generic advice like "validate input" but the exact validation to add

End with a **prioritized remediation plan** ordered by severity, and note any **false positives** explicitly with reasoning.

## When Information is Insufficient

If no file path or directory is specified, audit the entire project starting from the most security-sensitive areas (auth, API routes, data handling). If the tech stack is ambiguous, scan for all known vulnerability patterns across languages.

## Constraints

- Every finding MUST include a specific, implementable code fix
- False positives MUST be explicitly noted and explained — never silently omit them
- Do not modify any code — this is a read-only audit
- If compliance markers exist (SOC2, HIPAA, PCI-DSS), note which findings are compliance-relevant
