---
description: Perform a security audit of code to identify vulnerabilities and security issues
argument-hint: code to audit or project directory
allowed-tools: Read, Grep, Glob, Task
---

# Security Audit & Vulnerability Assessment

## Instructions

I'll perform a comprehensive security audit of the following code or project:

```
$ARGUMENTS
```

## Security Analysis Process

1. **Vulnerability Scanning**
   - OWASP Top 10 vulnerabilities
   - Language-specific security issues
   - Framework-specific security patterns
   - Authentication and authorization flaws
   - Input validation weaknesses
   - Output encoding issues
   - Configuration security

2. **Secure Coding Practices**
   - Data handling security
   - Cryptography implementation
   - Secure communication
   - Session management
   - Error handling and information leakage
   - Password policies and storage
   - Secrets management

3. **Access Control Analysis**
   - Authorization mechanisms
   - Permission models
   - Privilege escalation vectors
   - Role-based access control implementation
   - Authentication workflows

4. **Data Security Assessment**
   - Data encryption in transit
   - Data encryption at rest
   - PII/PHI handling
   - Data minimization
   - Retention policies
   - Logging security

## Detailed Findings

For each vulnerability:
1. Issue description and location
2. Severity rating (Critical, High, Medium, Low)
3. OWASP category or CWE reference
4. Potential exploit scenarios
5. Recommended fix with code example

## Risk Assessment

### Critical Vulnerabilities
- Immediate action items
- Potential impact
- Exploit likelihood

### Security Debt
- Architectural security issues
- Technical debt with security implications
- Systemic patterns

## Remediation Plan

### Immediate Fixes
- Critical vulnerability patches
- Quick security wins

### Short-term Improvements
- High-priority security enhancements
- Security control implementations

### Long-term Security Strategy
- Security architecture improvements
- Security testing integration
- Developer security training recommendations

## Verification Strategy
- Security testing approach
- Validation methods
- Ongoing security monitoring