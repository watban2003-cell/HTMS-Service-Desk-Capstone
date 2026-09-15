# Cost and Latency Benchmarks

## Project

HTMS Service Desk Capstone

## Benchmark Goal

The purpose of this benchmark is to verify that cost and latency optimizations do not reduce application quality.

All optimization steps must continue to pass the project's evaluation and regression gate.

## Baseline and Optimized Measurements

| Configuration | Cost | Latency | Cache | Evaluation |
|---|---:|---:|---|---|
| Baseline request | Measured in notebook | Measured in notebook | Cold | PASS |
| Cached request | Lower/equal cost | Lower/equal latency | Warm | PASS |
| Cost accounting demo | $0.000380 | N/A | N/A | PASS |

## Evaluation Requirement

Each optimization is accepted only when the golden-set regression gate continues to pass.

The optimization workflow is:

Baseline → Measure → Optimize → Re-run evaluation → Accept only if PASS

## Measurements

The notebook records:

- input token usage
- output token usage
- estimated request cost
- request latency
- cache behavior
- evaluation status

## Stable Prefix and Volatile Tail

Prompt construction should keep reusable content at the beginning of the prompt and request-specific content at the end.

Stable prefix examples:

- system instructions
- tool definitions
- service policies
- routing rules

Volatile tail examples:

- current user request
- request-specific context
- timestamps

This ordering improves the opportunity for provider-side prompt caching.

## Verification

Module 6 was re-run after fixing the runtime import dependency.

The cost accounting cell now produces a successful measured result:

`Cost accounting demo: $0.000380`

The final application should only accept performance optimizations when the evaluation gate remains PASS.

## Known Limitations

- Provider-side cached token usage is not currently available from the mock transport.
- Production benchmarks should use provider-reported cached token counts.
- Current measurements are course demonstration measurements rather than production load tests.
