# Backend Overview

GAINS uses Firebase as a managed backend foundation with server-side orchestration for AI features.

## Why Firebase

Firebase was selected to optimize for mobile delivery speed while maintaining a production-capable backend baseline:

- integrated authentication,
- managed document database,
- serverless function execution,
- and straightforward client SDK integration.

This lets product development focus on user workflows instead of infrastructure plumbing.

## Backend Responsibilities

### Authentication

- User identity and session handling.
- Access scoping for user-specific data.

### Data Storage (Firestore)

- Persistent records for nutrition logs, hydration events, body metrics, workouts, and profile goals.
- Query patterns designed around mobile read/write access paths.

### Cloud Functions

- Privileged workflows and backend-only logic.
- AI provider mediation.
- Request shaping, response normalization, and policy boundaries.

## Client vs Backend Separation

### Client handles

- UI rendering and interaction.
- View state and local input validation.
- Calling service abstractions for domain actions.

### Backend handles

- Secrets and provider credentials.
- Privileged orchestration logic.
- Controlled integration with external AI services.
- Backend validation and response gating.

This separation reduces sensitive surface area in the mobile app and improves maintainability.

## AI Request Mediation Pattern

Instead of direct client-to-provider calls:

1. Client sends a structured coaching request to a secure backend endpoint.
2. Backend enriches request with allowed user context.
3. Backend sends constrained request to OpenAI.
4. Backend sanitizes/normalizes response.
5. Client receives display-ready result.

Benefits:

- secure key management,
- centralized policy enforcement,
- easier observability and future cost/rate controls.

## Data and Security Posture (High-Level)

- Principle of least privilege for data access paths.
- Sensitive configuration remains outside source-controlled public artifacts.
- Public showcase excludes private backend internals and credentials.

## Scalability Considerations

As usage grows, expected evolution areas include:

- query/index refinement,
- background aggregation jobs,
- response caching strategies for repeated AI intents,
- and tighter observability around latency and error budgets.

## Public Scope Limitations

This document intentionally omits:

- production endpoint names,
- security rule internals,
- environment structure and key handling specifics,
- operational dashboards and incident details.
