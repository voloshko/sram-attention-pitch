# Accelerator Application Narrative

## What Are You Building?

We are building a CPU-only inference runtime for small 1-bit / 1.58-bit models.
It runs on ordinary ARM CPUs and uses cache residency instead of GPUs or
vendor-specific NPUs.

The first product is an OpenAI-compatible small-model endpoint that can run on
cheap ARM cloud machines. The long-term product is a portable runtime across
cloud ARM, Mac, Windows ARM, and Android.

## What Problem Do You Solve?

AI teams are paying GPU prices for many tasks that do not need frontier models:

- classification;
- extraction;
- routing;
- query rewriting;
- summarization;
- support-response drafts;
- RAG follow-up.

These tasks need useful tokens, not necessarily the largest model. We make
those tokens cheaper by running low-bit models on CPUs.

## Why Is This Possible Now?

Low-bit models changed the economics. At 1-bit / 1.58-bit, the bottleneck is
less about raw FLOPS and more about memory hierarchy: cache locality, bit decode,
hot metadata, activation LUTs, and thread scheduling. That is a different
engineering problem from normal dense GPU inference.

ARM CPUs are also everywhere now: Apple Silicon, Android phones, Windows ARM
laptops, and cloud ARM instances from AWS, Google, Azure, and Oracle.

## Why This Team / Project?

The private engineering repo already has:

- MS BitNet and Bonsai runtime lanes;
- Rust REST integration;
- OpenAI-compatible and Anthropic-compatible API surfaces;
- platform profiling and startup autotune;
- cache-residency and low-bit kernel work;
- a spec-driven optimization process with postmortems for failed experiments.

This is not only a pitch. It is an engineering program with measured progress
and a clear product path.

## Current Traction

- MS BitNet Rust REST path: around 60+ tok/s warm 16-token generation on Apple
  Silicon class hardware.
- Bonsai REST path: around 40 tok/s generation.
- Oracle ARM free-tier synthetic probe: around 5.9-6.3 tok/s for an
  MS-BitNet-shaped projection workload without model files.
- Reproduced local MS BitNet lane showed the Rust path around 2-3x faster than
  the original/native baseline in our project environment.

## What Do You Need From An Accelerator?

- Cloud credits across ARM providers.
- Introductions to ARM, Android, and cloud infrastructure teams.
- Design partners with high-volume small-model workloads.
- Help turning a research runtime into a hosted product.
- Fundraising support for the Android SDK and production serving milestones.

## 12-Month Goal

Become the default cheap CPU inference layer for small low-bit models:

- public ARM cloud benchmark matrix;
- hosted endpoint private beta;
- Android SDK prototype;
- Windows ARM and macOS binary releases;
- model partner integrations.

## The Big Vision

The AI market will not be served only by giant GPU models. It will also contain
millions of small specialized models running close to users, data, and product
workflows. `sram_attention` is infrastructure for that second branch.

