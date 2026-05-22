# Product-Market Fit Research

## Verdict

The strongest product-market fit is **cheap always-on small-model inference on
ARM CPUs**, sold first as a hosted or self-hosted OpenAI/Anthropic-compatible
endpoint for background agent work, routing, extraction, summarization, and
private deterministic assistants.

The latest technical progress materially improves the PMF story:

- Falcon3-1B now reaches laptop-class `~100 tok/s`, Oracle A1 `~30 tok/s`, and
  Google C4A/Axion `~44 tok/s` without GPUs.
- The runtime supports four model families: MS BitNet, Bonsai, Falcon3, and a
  ModernBERT Diff lane.
- The project has moved from hand-tuned kernels to a repeatable optimization
  machine: primitive catalog, physical planner, 5x3 fanout races, Git-persisted
  physical plans, leaderboard history, and adaptive platform cost learning.

That combination is the market signal. The buyer is not paying only for one
model. The buyer is paying for a system that can keep finding cheap, practical
low-bit inference paths as ARM CPUs and native 1-bit models improve.

## PMF Scorecard

| Segment | Fit now | Fit if next milestones land | Why |
|---|---:|---:|---|
| Cloud ARM small-model serving | 8.5/10 | 9/10 | Strongest wedge: clear cost pain, simple deployment, measured Oracle + Google ARM full-model results |
| Agent background workers | 8/10 | 9/10 | Slow-agent tasks tolerate seconds of latency and value low cost, privacy, and always-on capacity |
| Low-bit inference optimizer / compiler | 7.5/10 | 9/10 | Physical planner, primitive dictionary, and proof-carrying story are differentiated and defensible |
| Mac / Windows ARM local runtime | 7/10 | 8/10 | Strong privacy/dev story; needs polished binaries and coherent text-generation admission |
| Android on-device SDK | 6.5/10 | 8.5/10 | Huge distribution, but thermal policy, packaging, and OEM/app channels are harder |
| Medical imaging CV kernels | 6.5/10 | 8/10 | Strong adjacency if proof-backed image primitives and auditable pipelines land |
| Dense coding-model serving | 6/10 | 7/10 | Qwen3.6 GPU lane proves harness skill, but it is adjacent to the CPU-only core wedge |
| Replacing all GPU inference | 2/10 | 3/10 | Wrong category; frontier/high-batch workloads stay GPU/NPU-first |

## External Market Signals

The market has moved in our direction:

- **Cloud ARM is mainstream.** Google C4A uses Axion/Neoverse V2, supports up to
  72 vCPUs and 576 GB memory, and has no SMT: one vCPU maps to one physical
  core. That is exactly the kind of predictable core allocation our CPU kernels
  need.
- **New Google N4A and Axion expansion confirm the platform trend.** N4A is a
  newer Neoverse N3 family with larger shapes, and Arm/Google are explicitly
  positioning Axion as a consistent infrastructure base for AI and agentic
  workloads.
- **Oracle A1 is an unusually strong experimentation wedge.** OCI's Always Free
  tier includes Ampere A1 ARM compute hours and memory-hours, creating a
  zero-cost base for slow-agent and developer experiments.
- **Azure Cobalt and AWS Graviton make ARM multi-cloud.** Azure Cobalt exposes
  one physical core per VM vCPU, while Graviton instances are already supported
  by AWS inference services and SageMaker deployment paths.
- **Device ARM continues to improve.** Qualcomm's latest flagship mobile
  platform advertises a 4.6 GHz CPU variant and faster on-device AI blocks,
  while Windows ARM/Copilot+ PCs keep expanding the laptop deployment surface.

Sources: Google C4A/N4A docs, Google Axion product pages, Oracle Always Free
resources, Azure Cobalt docs, AWS Graviton/SageMaker docs, Qualcomm Snapdragon
8 Elite Gen 5 materials.

## Best Initial Market

The best initial market remains **cloud ARM small-model serving**, with a more
specific ICP:

> AI teams that already use LLMs for many small, repetitive calls and want a
> cheap, private, OpenAI-compatible endpoint for the calls that do not justify a
> frontier GPU model.

Examples:

- routing;
- classification;
- extraction;
- query rewrite;
- summarization;
- policy checks;
- agent planning substeps;
- deterministic support snippets;
- overnight codebase triage and slow-agent work.

This segment has the best PMF because it has all five ingredients:

| Ingredient | Status |
|---|---|
| Clear pain | GPU-backed endpoints are expensive for small repetitive calls |
| Buyer can test quickly | Drop-in OpenAI/Anthropic-compatible endpoint |
| Technical proof | Falcon3-1B runs on Oracle and Google ARM at useful speed |
| Economic proof | Google C4A spot estimate is near ten euro-cents per 1M generated tokens before margin |
| Expansion path | Same runtime can move to Mac, Windows ARM, Android, and other ARM clouds |

## Product Shape

### First Product: Cheap Small-Model Endpoint

Offer:

- hosted or self-hosted Rust server;
- OpenAI-compatible `/v1/chat/completions`;
- Anthropic-compatible `/v1/messages`;
- Falcon3/MS BitNet class models first;
- deterministic/low-temperature serving first;
- platform profile and startup autotune;
- benchmark and request-wall telemetry.

Positioning:

> Route your cheap, repetitive AI calls to an ARM CPU endpoint instead of a GPU
> endpoint.

### Second Product: Optimization Layer

Offer:

- primitive dictionary;
- physical planner;
- model/platform leaderboard;
- 5x3 fanout optimization runs;
- customer hardware certification;
- "bring your low-bit model" optimization pass.

Positioning:

> We do not only run one model. We keep learning how each low-bit primitive
> behaves on each ARM platform, then build the cheapest physical plan.

### Third Product: Device SDK

Offer:

- Android NDK + Kotlin wrapper;
- macOS and Windows ARM binaries;
- local REST bridge;
- thermal/thread policies;
- model packaging.

Positioning:

> Private low-bit assistants on devices without vendor NPU lock-in.

## Why The New Planner Matters Commercially

The physical planner changes the PMF from "fast today" to "gets faster over
time."

```mermaid
flowchart LR
  A["Customer model + hardware"] --> B["Primitive catalog"]
  B --> C["Candidate physical plans"]
  C --> D["Fanout benchmark race"]
  D --> E["Integration gate"]
  E --> F["Leaderboard + cost ledger"]
  F --> G["Better default profile"]
  G --> C
```

This creates three forms of moat:

- **Technical moat:** each primitive gets measured, priced, and reused.
- **Data moat:** every customer/platform run improves the planner memory.
- **Trust moat:** failed optimizations are preserved as postmortems, not hidden.

The `attention-score-neon-on` Falcon3 result is the first clean example. A new
component entered the dictionary, won a full-path race by `+7.03%`, and can now
be reused in later plans. The failed `f32-coherent-control` plan is equally
valuable: it teaches the planner that a conservative coherence path is a
diagnostic guardrail, not a performance default.

## Jobs To Be Done

### JTBD 1: Reduce AI Bill For Simple Calls

"When my app makes thousands or millions of simple model calls, I want to route
the easy ones to a cheap endpoint so my GPU/frontier bill stops growing
linearly with traffic."

Good buyer:

- AI SaaS founder;
- infra lead;
- RAG/product team;
- support automation team.

Adoption blocker:

- needs quality routing and fallback policy, not just raw speed.

### JTBD 2: Run Private Local Inference

"When data cannot leave the machine or VPC, I want a small local model with an
OpenAI-compatible API so existing tools still work."

Good buyer:

- enterprise team;
- health/finance/legal workflow vendor;
- developer-tool company.

Adoption blocker:

- needs coherent text-generation parity, model cards, and clear quality limits.

### JTBD 3: Make Weak Models Useful With Harness

"When a small model is not smart enough alone, I want a harness that gives it
tools, context, confidence policy, verification, and fallback."

Good buyer:

- agent framework team;
- internal automation team;
- developer productivity team.

Adoption blocker:

- needs polished orchestration examples and evidence that fallback saves quality.

### JTBD 4: Run Auditable Medical Imaging Pipelines

"When image processing supports a medical workflow, I want fast, cache-friendly
CV primitives with stronger proofs, traceable outputs, and clear quality
bounds."

Good buyer:

- medical imaging software team;
- device or workflow vendor;
- healthtech platform team.

Adoption blocker:

- needs stronger correctness evidence, reproducibility, and validation against
  existing clinical or preprocessing pipelines.

## Competitive Read

| Competitor class | Strength | Weakness / opening |
|---|---|---|
| GPU inference providers | Best quality, high batch throughput | Expensive and overpowered for simple always-on calls |
| llama.cpp / generic runtimes | Huge model coverage and community | Not narrowly optimized for cache-resident native 1.58-bit ARM serving |
| Native BitNet stacks | Reference ecosystem | Less productized around REST, cloud economics, planner memory, and multi-model champion race |
| Vendor NPUs | Efficient on supported devices | Fragmented APIs, weaker portability, hard cloud story |
| Edge AI platforms | Distribution and SDKs | Often model/runtime agnostic; less proof around 1-bit cache-resident kernels |

Best response: do not compete as a generic runtime. Compete as the **low-bit ARM
inference optimizer and serving stack**.

## Pricing Hypotheses

| Product | Possible pricing | What validates it |
|---|---|---|
| Hosted small-model endpoint | per 1M generated tokens with clear discount vs GPU-backed small-model APIs | Customers route real simple calls and keep using it after free trial |
| Self-hosted ARM binary | monthly per deployed instance or annual license | Teams want private/VPC deployment |
| Optimization pass | fixed-fee certification per model/platform | Customers bring a model/hardware target and pay for speedup |
| Enterprise SDK | annual support + integration fee | Android/Windows/enterprise teams need packaging and support |

The likely first paid product is not a giant platform subscription. It is a
specific endpoint or optimization pass with a before/after benchmark.

## PMF Risks

| Risk | Severity | Mitigation |
|---|---:|---|
| Text-generation quality is not admitted for every fast model | High | Treat Falcon/MS BitNet/Bonsai speed and language quality as separate gates; publish only coherent model profiles |
| Small models may not satisfy general chat expectations | High | Sell narrow tasks and routed/fallback flows, not frontier replacement |
| Cloud ARM spot capacity can be interrupted | Medium | Offer self-hosted/on-demand profiles and queue-friendly background-worker use cases |
| Android thermal behavior may cut throughput | Medium | Delay Android as first revenue wedge; benchmark flagship devices after cloud PMF |
| llama.cpp absorbs some low-bit formats | Medium | Use llama.cpp as radar; differentiate on ARM profiles, planner memory, primitives, and product harness |
| Native 1.58-bit model supply may be uneven | Medium | Support MS BitNet, Falcon3, Bonsai, and keep scanning GGUF/IQ/TQ ecosystems |
| Buyer may not care about proof-carrying optimization | Low/Medium | Pitch proof layer to technical partners/investors; pitch cost and drop-in endpoint to buyers |

## PMF Tests For The Next 30 Days

1. **Hosted Falcon3-1B C4A beta.**
   - Goal: 3-5 design partners route non-critical simple calls.
   - Success: at least one partner runs sustained traffic for a week.

2. **Quality-gated model profiles.**
   - Goal: label model profiles as `fast-coherent`, `fast-token-id-only`,
     `diagnostic`, or `research`.
   - Success: no benchmark is presented as language-ready unless it passes
     generation parity and prompt tests.

3. **Cost calculator landing page.**
   - Goal: show tokens/month and cost/1M by provider/profile.
   - Success: visitors can compare GPU endpoint spend vs ARM endpoint estimate
     in under one minute.

4. **One optimization-pass case study.**
   - Goal: show baseline -> physical planner -> 5x3 fanout -> promoted
     primitive -> improved endpoint.
   - Success: the `NeonAttentionScore` story becomes a reusable sales artifact.

5. **OpenAI/Anthropic compatibility demo.**
   - Goal: one CLI/tool harness talking to the local/ARM endpoint.
   - Success: a buyer sees their existing code work without SDK migration.

6. **Cloud provider benchmark matrix.**
   - Goal: Oracle A1, Google C4A/N4A, AWS Graviton, Azure Cobalt.
   - Success: identify one default commercial SKU and one fallback SKU.

## Recommended Wedge

Do this first:

> Launch a private beta for cheap ARM-hosted Falcon3/MS BitNet endpoints with
> OpenAI/Anthropic compatibility, visible cost-per-token, and a planner-backed
> optimization report for each hardware/model profile.

Do not lead with:

- "we replace GPUs";
- "we beat frontier models";
- "we run every model format";
- "formal verification proves model quality."

Lead with:

- "cheap useful tokens";
- "CPU-only low-bit serving";
- "drop-in endpoint";
- "planner that learns from every benchmark";
- "cloud ARM today, device ARM tomorrow."

## Sources

- [Google Compute Engine CPU platforms](https://docs.cloud.google.com/compute/docs/cpu-platforms)
- [Google Compute Engine general-purpose machine family](https://cloud.google.com/compute/docs/general-purpose-machines)
- [Google Axion processors](https://cloud.google.com/products/axion)
- [Oracle Always Free resources](https://docs.oracle.com/en-us/iaas/Content/FreeTier/freetier_topic-Always_Free_Resources.htm)
- [Oracle OCI Ampere A1 Compute](https://www.oracle.com/cloud/compute/arm/)
- [Azure Cobalt processor-based VMs](https://learn.microsoft.com/en-us/azure/virtual-machines/sizes/cobalt-overview)
- [AWS Graviton-based SageMaker inference](https://aws.amazon.com/blogs/machine-learning/run-machine-learning-inference-workloads-on-aws-graviton-based-instances-with-amazon-sagemaker/)
- [Qualcomm Snapdragon 8 Elite Gen 5](https://www.qualcomm.com/smartphones/products/8-series/snapdragon-8-elite-gen-5)
