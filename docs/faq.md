# FAQ

## Is this a replacement for GPUs?

No. It is a cost-effective path for small low-bit models and deterministic
workloads where GPUs are economically overpowered.

## Why not use mobile NPUs?

NPUs are powerful but fragmented. Qualcomm, MediaTek, Apple, Google, and
Samsung all expose different stacks. A CPU-first ARM NEON path is more portable
for the first product.

## Why low-bit models?

At 1-bit / 1.58-bit, weight bandwidth and cache residency become the central
problem. This creates a new optimization surface where CPUs can be surprisingly
competitive for small models.

## What is cache residency?

Cache residency means keeping the hot working set in fast CPU caches: activation
LUTs, scales, metadata, worker state, and current layer buffers. Packed cold
weights stream through predictable memory paths instead of forcing the whole
model into expensive accelerator memory.

## Why ARM?

ARM is everywhere: phones, Macs, Windows ARM laptops, and cloud servers. ARM
NEON is common enough to support a portable low-level kernel strategy.

## What is the first customer use case?

Cheap small-model serving:

- extraction;
- classification;
- routing;
- query rewriting;
- summarization;
- RAG follow-up;
- deterministic assistant commands.

## What is still missing?

- public cloud ARM full-model benchmark matrix;
- Android SDK;
- production-grade streaming server;
- public cost-per-token dashboard;
- more model quality evaluation.

