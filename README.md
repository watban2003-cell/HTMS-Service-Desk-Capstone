# HTMS Service Desk Capstone

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1VtneQSr9Hzxmxdfsimm2MF-gm55y8cwT?usp=drive_link)

This project is a capstone implementation for the LLM Application Engineering course.

The notebook demonstrates a Healthcare Technology Management Services (HTMS) service desk assistant that can classify, route, validate, and evaluate user requests.

## Main Capabilities

The application supports:

- FAQ requests
- Service requests
- Escalations
- Safety-sensitive requests
- Prompt injection detection
- PII masking
- Structured request handling
- Regression testing
- Cost and latency measurement
- Response caching

## Main Notebook

`HTMS_Service_Desk_Capstone_Final.ipynb`

## How to Run

1. Click the **Open in Colab** badge above.
2. Open the notebook in Google Colab.
3. Select:

   `Runtime → Run all`

4. Allow all cells to complete.
5. Confirm that the verification and evaluation cells complete without errors.
6. Review the final outputs for:
   - routing
   - guardrails
   - evaluation
   - regression gate
   - cost accounting
   - latency measurement
   - caching

## Project Architecture

The application uses a provider-neutral architecture with:

- LLM client boundary
- routing layer
- prompt pipeline
- safety guardrails
- structured outputs
- tool authorization
- evaluation harness
- regression gate
- cost and latency instrumentation

## Evaluation

The project includes a versioned golden set and deterministic evaluation harness.

The evaluation checks:

- expected routing behavior
- safety cases
- legitimate user requests
- regression detection
- overall accuracy thresholds

A deliberately broken configuration is also tested to verify that the regression gate correctly blocks degraded behavior.

## Cost and Latency Engineering

The notebook includes:

- token usage accounting
- estimated request cost
- latency measurement
- cache-aware request handling
- cold and warm execution checks

## Project Goal

The goal is to build a reliable, structured, measurable, and production-oriented LLM service desk assistant for Healthcare Technology Management Services.

## Known Limitations

- Some provider integrations are demonstrated using mock transports.
- The current project focuses on reproducible course demonstrations rather than production deployment.
- Further work can include real commercial provider integration, LLM-as-judge evaluation, and open-weight model benchmarking.
