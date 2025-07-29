---
description: Design comprehensive RESTful or GraphQL APIs with documentation
argument-hint: API requirements, domain model, and constraints
allowed-tools: Read, Task, Glob
---

# API Design & Documentation Generator

## Instructions

I'll create a comprehensive API design based on:

```
$ARGUMENTS
```

## Analysis Process

1. **Requirements Analysis**
   - Functional requirements identification
   - Data model examination
   - Access pattern analysis
   - Integration requirements
   - Performance expectations
   - Scaling considerations

2. **API Architecture Selection**
   - REST vs GraphQL vs Hybrid evaluation
   - Version strategy determination
   - Authentication mechanism selection
   - Rate limiting approach
   - Caching strategy

3. **Resource/Schema Design**
   - Entity identification
   - Relationship modeling
   - CRUD operation mapping
   - Query capability design
   - Mutation capability design
   - Subscription needs (if real-time)

## API Design Output

### API Architecture
- Protocol selection
- Communication patterns
- Authentication flow
- Authorization framework
- Error handling strategy
- Versioning approach

### REST API Design
- Resource hierarchy
- URI structure
- HTTP method usage
- Status code strategy
- Request/response format
- Collection pagination approach
- Filtering mechanism
- Sorting capabilities
- Field selection strategy

### GraphQL Schema Design
- Type definitions
- Query definitions
- Mutation definitions
- Subscription definitions
- Resolver structure
- Input validation
- Directive usage
- Error handling strategy
- N+1 query prevention

### Security Design
- Authentication mechanisms
- Authorization rules
- Input validation approach
- Output sanitization
- Rate limiting strategy
- CORS configuration
- Data encryption requirements

### Performance Optimization
- Caching strategy
- Query optimization
- Connection pooling
- Response compression
- Batch operations
- Pagination implementation

## API Documentation

### OpenAPI/Swagger Specification
- Complete API specification
- Schema definitions
- Path configurations
- Security definitions
- Example requests/responses

### GraphQL Schema Documentation
- Type documentation
- Query documentation
- Mutation documentation
- Directive explanations
- Best practice guidelines

### Developer Guide
- Authentication guide
- Rate limiting explanation
- Error handling documentation
- Pagination guide
- Filtering examples
- Common use cases
- Integration code samples

### Implementation Recommendations
- Framework recommendations
- Middleware suggestions
- Validation strategy
- Testing approach
- Monitoring recommendations
- Documentation maintenance