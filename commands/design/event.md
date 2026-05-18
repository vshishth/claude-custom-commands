---
description: Event-driven architecture design — schemas, pub/sub, event flows
argument-hint: event or system description (e.g., "reservation created event", "order processing pipeline")
allowed-tools: Read, Grep, Glob, Bash(find:*, grep:*, cat:*, ls:*)
---

# Event Architecture Design

Act as a Principal Engineer designing event-driven systems. Produce event schemas, flow diagrams, and implementation guidance for reliable asynchronous communication.

Existing event patterns:
!`grep -rl "event\|publish\|subscribe\|consumer\|producer\|kafka\|sqs\|sns\|nats\|rabbitmq\|EventBridge" --include="*.go" --include="*.ts" --include="*.yaml" -l 2>/dev/null | head -10`

Message infrastructure:
!`grep -r "kafka\|sqs\|sns\|nats\|rabbitmq\|eventbridge\|pubsub" --include="*.yaml" --include="*.tf" --include="*.json" 2>/dev/null | head -5`

```
$ARGUMENTS
```

## Process

1. **Identify event boundaries** — Determine which state changes should trigger events. Apply the rule: events represent facts that happened, not commands to execute.
2. **Design event schema** — Define the event structure: type, source, timestamp, correlation ID, payload. Use CloudEvents spec or project's existing schema convention.
3. **Map producers and consumers** — Identify who publishes each event and who reacts. Document the coupling (event-carried state transfer vs event notification).
4. **Design delivery guarantees** — Specify: at-least-once vs exactly-once semantics, ordering requirements, retry policy, dead-letter queue handling.
5. **Handle failures** — Design idempotency strategy, poison message handling, compensating events for saga patterns.

## When Information is Insufficient

If the messaging infrastructure is unknown, ask or recommend based on requirements (SQS for simple queues, Kafka for streaming, EventBridge for event routing). If event boundaries are unclear, analyze the domain model for aggregate boundaries.

## Output

### Event Catalog
| Event | Producer | Consumers | Schema Version |
|-------|----------|-----------|---------------|

### Event Schema
```json
{
  "type": "reservation.created",
  "source": "reservation-service",
  ...
}
```

### Flow Diagram (ASCII)
```
[Producer] --event--> [Topic/Queue] --delivers--> [Consumer]
```

### Delivery Guarantees & Error Handling
- Idempotency strategy
- DLQ configuration
- Retry policy

## Constraints

- Events MUST be past-tense facts ("OrderCreated"), not imperative commands ("CreateOrder")
- Events MUST include a correlation/trace ID for distributed tracing
- Event schemas MUST be versioned — breaking changes require a new event type
- Consumers MUST be idempotent — at-least-once delivery means duplicates happen
- NEVER put sensitive data (PII, secrets) in event payloads without explicit encryption
- Include schema evolution strategy (backward compatible additions, deprecation path)
