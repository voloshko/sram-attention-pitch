# Public Status

`sram_attention` is a Rust runtime strategy for cache-resident, low-bit model
inference on ARM CPUs. This page is the public status view: what is live, what
has been measured, and what is next.

## Status at a Glance

| Area | Status | Public signal |
|---|---|---|
| Core runtime | Live | CPU-only low-bit inference for small models |
| Serving | Live | OpenAI-compatible and Anthropic-compatible APIs |
| Model families | Live | MS BitNet, Bonsai, Falcon3, ModernBERT Diff |
| Platform autotune | Live | Apple Silicon, Oracle A1, Google C4A/N4A, other ARM hosts |
| Champion history | Live | Git-backed race log with measured winners and failures |
| Scientific rationale | Live | Winning plans carry a human-readable `why` |
| Public benchmark story | Live | Repeatable, comparable, and versioned in Git |

## What Is Publicly Proven

| Platform | Model path | Public result |
|---|---:|---:|
| Apple M3 Pro | Falcon3-1B native 1.58-bit | ~96.9 tok/s warm REST |
| Apple M3 Pro | MS BitNet Rust REST | ~60.9 tok/s warm generation |
| Oracle A1 | Falcon3-1B native 1.58-bit | ~30.2 tok/s warm REST |
| Google C4A/Axion | Falcon3-1B native 1.58-bit | ~44.0 tok/s warm REST |
| Google C4A/Axion | MS BitNet / Falcon3 sweep | platform-specific primitive pricing validated |
| Apple M3 Pro | Champion history | `why` column now explains winning plans in plain language |

## What the Product Actually Is

- a low-bit model runtime for small models that fit the CPU/cache cost curve;
- a planner that learns which primitive is worth using on which platform;
- a public history of races, regressions, and winners;
- a repeatable way to turn a benchmark win into a reusable primitive;
- a proof-grounded explanation layer for investor and partner review.

## Why It Matters

Most AI systems rent expensive GPU capacity for every token. This project is
designed for a different economy: keep the hot working set close to the CPU,
stream packed low-bit weights, and use cheaper ARM machines for small but
useful workloads like routing, extraction, summarization, and slow-agent
background work.

The public story is intentionally auditable:

- winning plans are persisted in Git;
- failed ideas stay visible as part of the learning record;
- the champion history shows `before`, `after`, `delta`, and `why`;
- the planner can explain its choices without exposing private implementation.

## How It Works

| Step | Public meaning |
|---|---|
| Model family | Falcon3, MS BitNet, Bonsai, and ModernBERT Diff are all part of the same optimization story |
| Primitive dictionary | Useful acceleration ideas are measured, named, and reused |
| Physical planner | The system chooses the best plan for the current hardware |
| Champion history | Every win and loss is kept in Git so the story stays auditable |
| Scientific rationale | Each winning plan gets a short human-readable `why` |

## Current Direction

| Direction | What is next |
|---|---|
| Cloud ARM serving | Expand the benchmark matrix across Oracle, Google, AWS, and Azure ARM hosts |
| Device runtime | Continue Mac and Windows ARM readiness and Android packaging |
| Public proof | Keep the champion log, rationale column, and benchmark story synchronized |
| Productization | Continue shaping a cheap small-model endpoint and private deployment story |

## Links

- [README overview](../README.md)
- [Go-to-market notes](go-to-market.md)
- [Investor one-pager](investor-one-pager.md)
- [Benchmark story](benchmark-story.md)
