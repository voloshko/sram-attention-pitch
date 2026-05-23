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
| Dynamic host lanes | Live | Python server and browser/Wasm flows patch formulas around the same verified primitives |
| Champion history | Live | Git-backed race log with measured winners and failures |
| Scientific rationale | Live | Winning plans carry a human-readable `why` |
| Public benchmark story | Live | Repeatable, comparable, and versioned in Git |
| Image/CV lane | Live | The same playbook now turns image work into millisecond-scale hot paths and a browser/GPU delivery lane |

## What Is Publicly Proven

| Platform | Model path | Public result |
|---|---:|---:|
| Apple M3 Pro | Falcon3-1B native 1.58-bit | ~96.9 tok/s warm REST |
| Apple M3 Pro | MS BitNet Rust REST | ~60.9 tok/s warm generation |
| Apple M3 Pro | Image/CV native path | slow full-image work turned into millisecond-scale hot crops |
| Browser demo | WASM + WebGPU CV lane | browser delivery now shows a real GPU acceleration path on larger images |
| Oracle A1 | Falcon3-1B native 1.58-bit | ~30.2 tok/s warm REST |
| Google C4A/Axion | Falcon3-1B native 1.58-bit | ~44.0 tok/s warm REST |
| Google C4A/Axion | MS BitNet / Falcon3 sweep | platform-specific primitive pricing validated |
| Apple M3 Pro | ModernBERT donor hot path | ~3.15x faster than cold API compare |
| Python server | Dynamic ITA + Redness API | live formula fetch-edit-patch with split hot timings |
| Browser demo | Dynamic ITA + Redness formula | editable JS on top of Wasm, SIMD, and WGPU |
| Apple M3 Pro | Champion history | `why` column now explains winning plans in plain language |

## What the Product Actually Is

- a low-bit model runtime for small models that fit the CPU/cache cost curve;
- a planner that learns which primitive is worth using on which platform;
- dynamic languages that stitch fast verified CV + LLM primitives into product surfaces without re-implementing the math each time;
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
- the donor-primitive ModernBERT experiment showed that optimized words from
  other models can speed up a new lane by more than 3x without breaking
  correctness;
- the image/CV lane showed the same idea again: we took a slow native path,
  made the hot crop millisecond-fast, and then opened a browser/GPU delivery
  lane on top of it;
- the same primitive story now works as a dynamic product surface in both a
  Python server flow and a Wasm/browser flow;
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
| Image/CV primitives | Prototype proof-backed image/CV micro-kernels for medical imaging and other CV workloads |

## Adjacent Pitch Surface

The same primitive discipline can widen beyond LLM inference:

- image/CV methods now have their own primitive space, separate from the LLM kernel namespace;
- stronger proof layers can be attached to each primitive and composition law;
- the first proof-backed micro-kernel bridge has already landed in the engineering repo;
- medical imaging is a strong commercial adjacency because correctness,
  traceability, and reproducibility matter there even more than in general
  consumer image processing.

We move image processing from fixed-function speed to composable, verified,
server-grade pipelines.

## Links

- [README overview](../README.md)
- [Go-to-market notes](go-to-market.md)
- [Investor one-pager](investor-one-pager.md)
- [Benchmark story](benchmark-story.md)
