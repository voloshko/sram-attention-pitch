---
id: PUBLIC-IMPL-002
title: REST integration validity gate
status: verified
---

# REST Integration Validity Gate

## Goal

Prove that the direct benchmark is representative of product-shaped serving.

## Problem

Microbenchmarks and direct loops can hide product overhead:

- tokenizer;
- JSON parsing;
- request lock;
- response formatting;
- runtime state setup;
- HTTP server overhead.

## Acceptance Criteria

- Run the direct benchmark and REST benchmark on the same model and token count.
- Record generation tok/s and request-wall tok/s separately.
- If REST generation is slower by more than the threshold, future claims must
  include both numbers.

## Decision

Keep. Product-facing performance claims must not rely only on a clean direct
benchmark.

