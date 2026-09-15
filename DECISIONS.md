# Architecture Decisions

## Project

HTMS Service Desk Capstone

## 1. Provider-Neutral LLM Boundary

The application uses an `LLMClient` protocol boundary so the rest of the application does not depend directly on one model provider.

This design was chosen to:

- keep business logic provider-neutral
- simplify testing with mock transports
- allow commercial or open-weight providers to be added later
- reduce vendor lock-in

## 2. Router-First Design

The application routes requests before applying downstream processing.

This design was chosen because different request types require different handling.

Examples include:

- FAQ requests
- Service requests
- Escalations
- Safety-sensitive requests

Routing early allows the application to apply the appropriate prompt, guardrails, tools, and escalation logic for each request type.

## 3. Provider Adapters

Provider adapters are used to isolate provider-specific request and response formats from the application core.

The current capstone demonstrates provider-shaped adapters using mock transports for reproducible testing.

A production implementation can replace the mock transport with a real OpenAI-compatible, Anthropic, or other provider SDK without changing the core application logic.

## 4. Retry and Fallback Strategy

Retry and fallback behavior is implemented at the model boundary.

Retry is limited to retryable failures, while non-retryable failures stop immediately.

Fallback routes allow the application to attempt an alternative model or provider when the primary route fails.

This approach improves resilience while keeping failure behavior explicit and bounded.

## 5. Structured Outputs

Structured outputs are used for service requests so downstream application logic does not rely on free-form text alone.

The current implementation validates structured request data before tool execution.

A future production version should use provider-native strict JSON schema generation with a Pydantic model.

## 6. Prompt Versioning

Prompts are versioned so prompt changes can be evaluated and compared.

Prompt versions are included in evaluation and caching logic to prevent results from different prompt versions from being mixed.

A future version can move prompt content into separate files under a `prompts/` directory.

## 7. Safety and Guardrails

The prompt pipeline includes:

- prompt injection detection
- PII masking
- output canary checks
- authorization checks before tool execution

The goal is to apply deterministic safety checks around the probabilistic model boundary.

## 8. Evaluation Before Release

Changes are evaluated against a versioned golden set before they are accepted.

A regression gate blocks configurations that fall below required quality or safety thresholds.

This makes evaluation part of the release process rather than an optional final check.

## 9. Cost and Latency

Cost and latency are measured at the model boundary.

This allows optimization techniques such as caching and routing to be compared without changing the rest of the application.

Any optimization should be accepted only if the evaluation gate still passes.

## 10. Model Selection Trade-off

The capstone currently prioritizes:

- reproducibility
- provider-neutral architecture
- deterministic testing
- low dependency on external services

Because of this, mock provider transports are used for several demonstrations.

For production deployment, the next step would be to compare:

- a commercial hosted model
- an open-weight self-hosted model

using the same golden set, latency measurements, and cost model.
