# Transversal-Stutter-Mitigation-Hypothesis
A hypothesis proposing the mitigation of residual gaming microstutters through configurable presentation buffering inspired by network jitter buffers.
# Transversal Stutter Mitigation Hypothesis

**Author:** Rodrigo Lagos  
**Initial Publication:** 2026-10-16  
**Status:** Technical Hypothesis / Open Discussion

---

# Abstract

Despite significant advances in shader precompilation, PSO caching, frame pacing, low-latency rendering, and technologies such as NVIDIA Reflex, modern games still exhibit residual microstutters that are perceptible even on high-end systems.

This document proposes a conceptual hypothesis inspired by network jitter buffers.

Instead of eliminating every source of microstutter, it may be possible to absorb a portion of residual frame-time variance through a configurable presentation buffer operating at the display output stage.

The primary objective is not reducing latency.

The primary objective is reducing visible frame-time irregularity.

---

# Background

Current approaches focus on preventing stutters by addressing their root cause:

- Shader precompilation
- PSO generation and caching
- Asset preloading
- Improved scheduling
- Frame pacing optimization
- Low latency render queues

These approaches are effective, especially against large stutters caused by first-time shader compilation.

However, residual microstutters often remain even after these systems are implemented.

Examples include:

- CPU scheduling variance
- GPU scheduling variance
- Driver overhead
- Frame delivery irregularities
- Synchronization issues
- Presentation timing anomalies

---

# Core Idea

The hypothesis is simple:

Instead of trying to eliminate every microstutter, hide small frame-time disturbances from the final presentation stage through a small configurable temporal buffer.

The inspiration comes from telecommunications.

In VoIP systems, packet arrival jitter is not eliminated.

Instead:

```text
Packets arrive irregularly
        ↓
Jitter Buffer
        ↓
Regularized playback
```

The user perceives a smoother output at the cost of a small amount of latency.

This document explores whether a similar concept could be applied to game rendering.

---

# Conceptual Model

Current Pipeline

```text
Input
 ↓
CPU
 ↓
GPU
 ↓
Presentation
 ↓
Display
```

Proposed Pipeline

```text
Input
 ↓
CPU
 ↓
GPU
 ↓
Presentation
 ↓
Micro Buffer
 ↓
Display
```

The micro buffer introduces a controlled delay before presentation.

---

# Proposed User Modes

## Competitive Mode

```text
5 ms Buffer
```

Minimal latency impact.

Designed for competitive environments.

---

## Balanced Mode

```text
10 ms Buffer
```

Balanced compromise between responsiveness and smoothness.

---

## Smooth Mode

```text
15 ms Buffer
```

Maximum microstutter absorption.

Designed for cinematic and single-player experiences.

---

# Example

Without Presentation Buffer

```text
Frame Times:

5 ms
5 ms
12 ms
5 ms
5 ms
```

Result:

```text
Visible Microstutter
```

---

With 15 ms Presentation Buffer

```text
Frame Times:

5 ms
5 ms
12 ms
5 ms
5 ms
```

Result:

```text
Microstutter absorbed within the temporal cushion.
```

The internal variance still exists.

The user simply does not perceive most of it.

---

# Scope

This hypothesis is NOT designed to solve:

```text
100 ms Shader Compilation Events
200 ms Asset Streaming Events
Major Engine Stalls
```

These issues should continue to be addressed through traditional methods.

Instead, this proposal targets:

```text
Residual 2-15 ms Microstutters
```

that remain after conventional optimizations.

---

# Why This May Be More Relevant Today

Historically, latency budgets were much larger.

Adding several milliseconds of additional delay could have been difficult to justify.

Today, modern gaming systems often operate with extremely low total latency.

Examples include:

- NVIDIA Reflex
- High refresh displays
- Ultra-low latency peripherals
- Modern rendering pipelines

Therefore, sacrificing:

```text
5 ms
10 ms
15 ms
```

for improved frame-time consistency may represent a more attractive tradeoff than in previous decades.

---

# Key Observation

Human perception may be more sensitive to latency variance than to a small amount of constant latency.

Example A

```text
25 ms
25 ms
25 ms
40 ms
25 ms
25 ms
```

Example B

```text
35 ms
35 ms
35 ms
35 ms
35 ms
35 ms
```

The second scenario introduces more latency but significantly less variability.

This document hypothesizes that many users may prefer the second experience.

---

# Relationship With Existing Solutions

This proposal is intended to complement, not replace:

- Shader precompilation
- PSO caching
- Asset preloading
- NVIDIA Reflex
- Engine-level optimizations

The ideal workflow would likely be:

```text
Large Stutters
↓
Prevent

Residual Stutters
↓
Absorb
```

---

# Open Questions

1. Has this concept already been explored in commercial engines?

2. Has any GPU vendor implemented a similar presentation-level buffer?

3. What is the measurable tradeoff between latency and smoothness?

4. Could this coexist with technologies such as NVIDIA Reflex?

5. What percentage of residual microstutters could realistically be hidden?

6. Could adaptive buffers outperform fixed-size buffers?

---

# Limitations

This document is currently a conceptual hypothesis.

No implementation exists at the time of publication.

No claims of effectiveness are made.

Experimental validation would be required.

---

# Discussion Invitation

This repository exists to encourage discussion among:

- Graphics programmers
- Engine developers
- Driver developers
- Frame pacing researchers
- Latency optimization specialists

Constructive criticism and technical feedback are welcome.

---

# Attribution

Original hypothesis proposed by:

**Rodrigo Lagos**

Publication date:

**2026-10-16**

This repository serves as the public timestamped publication of the concept.
