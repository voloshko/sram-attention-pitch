# Investor One-Pager

For a concise live status view, start with [public landing](public-landing.md).

## Company Thesis

Small low-bit models are becoming useful. GPUs are still priced for scarcity.
`sram_attention` makes small 1-bit / 1.58-bit models run fast on ordinary ARM
CPUs by using cache residency as the accelerator.

## Product

A Rust runtime and serving layer for CPU-only low-bit inference:

- MS BitNet b1.58 and Bonsai-style models;
- ARM NEON kernels;
- cache-resident hot working set;
- OpenAI-compatible and Anthropic-compatible REST endpoints;
- platform profiles for Mac, Android, Windows ARM, and cloud ARM.

## The Wedge

Do not start by replacing frontier GPU inference. Start with workloads where a
small local model is enough:

- classification;
- extraction;
- query rewrite;
- support answer drafts;
- routing;
- summarization;
- RAG follow-up;
- local assistant commands.

These workloads care about cost, latency, privacy, and operational simplicity.

## Evidence

| Evidence | Signal |
|---|---|
| MS BitNet Rust REST path around 60+ tok/s warm generation | Product-shaped path can be fast |
| Bonsai REST path around 40 tok/s generation | Larger low-bit path is credible |
| Oracle ARM synthetic probe around 6 tok/s without model files | Cheap ARM cloud can participate |
| 2-3x faster than reproduced original MS BitNet lane | Runtime/system work matters |
| Spec-driven optimization ledger | The team knows what failed and why |

## Why Now

- Low-bit models are no longer only a paper idea.
- ARM server CPUs are mainstream: Graviton, Axion, Cobalt, Ampere.
- Windows ARM and Android flagship SoCs are getting stronger.
- GPU costs are painful for small always-on inference.
- Enterprise buyers want private and local deployment options.

## Business Model

1. Hosted CPU-only endpoints for small low-bit models.
2. Enterprise SDK for local/private deployment.
3. Android / Windows ARM runtime licensing.
4. Benchmark and optimization services for customer models.

## Moat

- Cache-residency-first low-bit runtime design.
- Shared primitive layer across BitNet and Bonsai model families.
- Platform autotune for heterogeneous ARM devices.
- Spec-driven optimization process with postmortems, not folklore.
- REST integration that measures product overhead, not only microbenchmarks.

## Ask

Funding to ship:

- production REST server;
- public cloud ARM benchmark matrix;
- Android SDK and phone benchmarks;
- hosted low-cost small-model endpoint;
- model partner integrations.
