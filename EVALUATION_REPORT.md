# Evaluation Report

## Project

HTMS Service Desk Capstone

## Evaluation Approach

The project uses a versioned golden set and a deterministic evaluation harness to verify expected application behavior.

The evaluation covers:

- FAQ routing
- Service request routing
- Escalation routing
- Safety-sensitive requests
- Prompt injection detection
- Legitimate user requests
- Regression detection

## Golden Set

The evaluation set contains 18 test cases distributed across multiple behavioral categories.

Each test case defines:

- input
- expected behavior
- actual behavior
- pass/fail result

## Metrics

The evaluation reports:

- Overall accuracy
- Safety accuracy
- Legitimate-request accuracy
- Regression gate status

## Regression Gate

A threshold-based regression gate is used to prevent degraded versions from being accepted.

The notebook also includes a deliberately broken configuration to verify that the regression gate can detect and block regressions.

Expected behavior:

- Correct configuration → PASS
- Broken configuration → FAIL

## Current Evaluation Status

The final notebook includes evaluation and regression checks that complete successfully when the project is run end-to-end.

## Cost and Latency Verification

Module 6 includes:

- token usage accounting
- request cost estimation
- latency measurement
- cache behavior checks

The notebook was re-run after fixing the Module 6 runtime dependency so that cost and latency outputs are captured successfully.

## Known Limitations

The current evaluation has the following limitations:

- No LLM-as-judge evaluation is currently included.
- No human-label calibration study has been performed.
- Cohen's kappa is not currently reported.
- Some provider integrations use mock transports instead of live provider SDKs.
- Open-weight model benchmarking is not yet included.

## Future Improvements

Planned improvements include:

- Add an LLM-as-judge rubric.
- Add human-labeled calibration samples.
- Report agreement and Cohen's kappa.
- Compare commercial and open-weight backends.
- Add slice-level evaluation by request category.
