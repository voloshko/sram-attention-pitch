---
id: PUBLIC-IMPL-003
title: Rejected micro-optimization postmortem
status: obsolete
---

# Rejected Micro-Optimization Postmortem

## Goal

Try a plausible low-level kernel optimization.

## Hypothesis

Changing the inner-loop shape will reduce instruction overhead and improve
token throughput.

## Result

The isolated microbenchmark improved, but the full REST generation path did not.
The change increased instruction-cache pressure and made the product path
noisier.

## Decision

Reject. Roll back the code, keep the postmortem, and do not build further
optimizations on top of this path.

## Lesson

The full integration path is the source of truth. Microbench wins are only
accepted if they survive the product-shaped benchmark.

