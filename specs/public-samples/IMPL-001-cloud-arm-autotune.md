---
id: PUBLIC-IMPL-001
title: Cloud ARM startup autotune
status: verified
---

# Cloud ARM Startup Autotune

## Goal

Choose a safe first-run kernel mode and thread count on a new ARM cloud host
without downloading model weights.

## Problem

CPU feature flags alone do not predict the fastest low-bit inference path. A
host may expose dot-product instructions while a table-lookup kernel still wins
for the target shape.

## Scope

Allowed:

- model-free synthetic projection probe;
- provider profile names;
- printed benchmark ledger.

Out of scope:

- model download;
- production default promotion;
- provider-specific cloud APIs.

## Acceptance Criteria

- The probe runs without model files.
- It prints CPU model, provider hint, thread candidates, kernel candidates, and
  selected winner.
- It records the result in a spec or benchmark ledger.

## Decision

Keep. Startup autotune is necessary because static CPU detection is too weak for
portable low-bit kernels.

