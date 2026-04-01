---
description: Security audit identifying vulnerabilities with severity and fixes
argument-hint: file path, directory, or paste code
allowed-tools: Read, Grep, Glob, Bash
---

# Security Audit

Perform a security audit of the following code:

```
$ARGUMENTS
```

## Audit Scope

1. **Input validation** - Injection (SQL, NoSQL, command, XSS), path traversal, deserialization
2. **Authentication & authorization** - Auth bypass, privilege escalation, missing checks, session management
3. **Data protection** - Secrets in code, PII exposure, missing encryption, insecure storage
4. **Dependencies** - Known CVEs, outdated packages, supply chain risks
5. **Configuration** - Permissive CORS, debug mode in prod, insecure defaults, exposed endpoints
6. **Cryptography** - Weak algorithms, improper key management, predictable tokens

## Output

For each vulnerability:
- **Severity**: Critical / High / Medium / Low (use CVSS reasoning)
- **Location**: file:line
- **CWE**: Reference number if applicable
- **Issue**: What's wrong and how it could be exploited
- **Fix**: Specific code change to remediate

End with a prioritized remediation plan.
