---
description: Generate optimized Dockerfiles for different application types
argument-hint: application type, language, framework, and requirements
allowed-tools: Read, Task, Glob
---

# Dockerfile Generator

## Instructions

I'll create an optimized Dockerfile based on your application requirements:

```
$ARGUMENTS
```

## Analysis Process

1. **Application Requirements Analysis**
   - Language/framework identification
   - Runtime dependencies
   - Build-time requirements
   - Development vs production needs
   - Application architecture considerations

2. **Base Image Selection**
   - Official vs slim vs alpine comparison
   - Security considerations
   - Size optimization
   - Compatibility verification
   - Update frequency analysis

3. **Multi-stage Build Design**
   - Build stage optimization
   - Runtime stage minimization
   - Artifact selection strategy
   - Dependency pruning approach

## Dockerfile Generation

### Base Configuration
- Appropriate base image selection
- Environment variable configuration
- Working directory setup
- User security configuration
- Volume mount recommendations

### Dependency Management
- Optimized dependency installation
- Caching strategy for faster builds
- Version pinning strategy
- Security scanning integration

### Build Process
- Multi-stage build configuration
- Build argument management
- Compiler optimization flags
- Asset compilation strategy
- Test execution (optional)

### Runtime Configuration
- Minimal runtime environment
- Entry point configuration
- Health check implementation
- Signal handling setup
- Container lifecycle hooks

### Security Hardening
- Principle of least privilege implementation
- Attack surface minimization
- Sensitive data management
- User namespace configuration
- Read-only filesystem settings

### Performance Optimizations
- Layer optimization strategy
- Cache utilization approach
- Startup time optimization
- Resource constraint recommendations
- Garbage collection settings

## Additional Resources

### Docker Compose Configuration
- Development environment setup
- Service definitions
- Network configuration
- Volume management
- Local development workflow

### Documentation
- Image usage instructions
- Environment variables documentation
- Volume mount requirements
- Port exposure documentation
- Example commands

### CI Integration
- Build pipeline recommendations
- Automated testing strategy
- Image publishing workflow
- Tag versioning strategy
- Vulnerability scanning configuration