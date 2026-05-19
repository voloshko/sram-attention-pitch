# Technical Discipline

## Why Specs Matter

Performance engineering can become folklore quickly. `sram_attention` uses a
spec-driven optimization loop so that every major change has a clear hypothesis,
test, result, and decision.

## Loop

```mermaid
flowchart TD
    A["Profile real path"] --> B["Write hypothesis"]
    B --> C["Create bounded spec"]
    C --> D["Implement only the spec"]
    D --> E["Run benchmark"]
    E --> F{"Accept?"}
    F -->|Yes| G["Promote + document"]
    F -->|No| H["Rollback code"]
    H --> I["Keep postmortem"]
    I --> A
    G --> A
```

## Public Spec Shape

Each spec records:

- goal;
- problem;
- scope;
- acceptance criteria;
- benchmark plan;
- result;
- decision.

## Why This Is Investor-Relevant

This reduces execution risk. The team does not only collect wins; it preserves
negative evidence. That matters when pushing against hardware limits, where 90%
of plausible ideas do not survive measurement.

## What We Can Share Publicly

We can share:

- sanitized spec examples;
- benchmark methodology;
- accepted/rejected decision pattern;
- public results.

We do not share:

- proprietary source code;
- model artifacts;
- private customer workloads;
- unpublished implementation details.

