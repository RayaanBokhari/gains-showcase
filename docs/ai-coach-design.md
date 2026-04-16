# AI Coach Design (Public-Safe)

This document describes the AI coaching feature in conceptual and architectural terms without exposing private prompts or sensitive implementation details.

## Role of the AI Coach

The AI coach is designed to support user decision-making in nutrition and progress planning.

Primary responsibilities:

- Answer nutrition and macro-related questions.
- Suggest meal ideas aligned to user goals.
- Interpret recent user progress context at a high level.
- Offer actionable next-step recommendations.

It is intentionally assistive, not prescriptive clinical guidance.

## Example User Interactions

- "I’m low on protein today. What can I eat for dinner?"
- "How should I adjust macros if my weight trend is flat this week?"
- "Give me two high-protein snack ideas under 300 calories."
- "I missed workouts this week. What should I prioritize next week?"

## Conceptual Interaction Pipeline

1. User submits a question from the app.
2. Client sends request to backend function (not directly to provider).
3. Backend composes safe context envelope from user-scoped data.
4. Backend applies policy constraints and sends request to model provider.
5. Response is normalized/sanitized for app presentation.
6. Client renders coaching output with clear UX boundaries.

## Safety and Boundary Principles

- No exposure of provider API keys in client code.
- No unrestricted model access from the app.
- Context minimization: include only what is needed for useful responses.
- Avoid unsupported medical claims; position output as educational guidance.
- Prefer practical suggestions with transparent uncertainty where relevant.

## Personalization Strategy (High-Level)

Personalization is based on user-consented app context, such as:

- target goals,
- recent nutrition patterns,
- hydration trends,
- and workout consistency signals.

Personalization should remain controllable:

- users can update goals/preferences,
- context windows can be scoped,
- and future controls can expose personalization depth.

## Reliability Considerations

- Structured request/response shapes to reduce unpredictable outputs.
- Graceful fallback UX when AI responses fail or timeout.
- Clear error states and retry behavior.
- Logging/observability at backend boundaries (without sensitive payload leakage).

## What Remains Private (By Design)

To protect IP and security, the following are intentionally not published:

- production prompt templates and system instructions,
- provider tuning parameters and guardrail details,
- exact context assembly logic,
- abuse/risk heuristics,
- operational usage and cost thresholds.

## Future Evolution

- Better longitudinal personalization.
- More structured coaching plans (weekly macro/workout strategy).
- Improved memory controls and explainability.
- Expanded recommendation quality via richer analytics context.
