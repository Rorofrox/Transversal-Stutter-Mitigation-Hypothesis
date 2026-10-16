# Transversal-Stutter-Mitigation-Hypothesis
A hypothesis proposing the mitigation of residual gaming microstutters through configurable presentation buffering inspired by network jitter buffers.
Transversal Stutter Mitigation Hypothesis
Author: Rodrigo Lagos
Initial Publication: 2026-10-16

Abstract
Modern games continue to exhibit residual microstutters despite advances in shader precompilation, PSO caching, frame pacing optimization, low-latency rendering, and modern GPU scheduling.

This document proposes a conceptual hypothesis inspired by network jitter buffers.

Instead of attempting to eliminate every source of microstutter, a small configurable presentation buffer may absorb residual frame-time variance before it becomes visible to the user.

The objective is not reducing latency.

The objective is reducing visible frame-time irregularity.

The Core Idea
Current approaches generally focus on:

Prevent the stutter.
This hypothesis proposes exploring:

Absorb the stutter.
The inspiration comes from telecommunications.

In VoIP systems:

Irregular packet arrival
        ↓
     Jitter Buffer
        ↓
Regular output stream
The user receives a smoother experience at the cost of a small amount of latency.

This document explores whether a similar principle could be applied to frame presentation.

Problem Statement
Current solutions are effective against major stutters:

Shader compilation
PSO generation
Asset streaming stalls
However, residual microstutters often remain:

CPU scheduling variance
GPU scheduling variance
Driver overhead
Presentation irregularities
Minor synchronization issues
Residual frame pacing anomalies
These events frequently fall within:

2 ms
5 ms
10 ms
15 ms
and may still be visible to the user on high-refresh displays.

Proposed Solution
Introduce a small configurable presentation buffer operating immediately before display output.

Conceptually:

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
The micro buffer introduces a controlled temporal cushion.

Proposed User Profiles
Competitive
5 ms Buffer
Lowest latency impact.

Balanced
10 ms Buffer
Compromise between responsiveness and smoothness.

Smooth
15 ms Buffer
Maximum microstutter absorption.

Example
Without Buffer:

5 ms
5 ms
12 ms
5 ms
5 ms
Result:

Visible microstutter
With 15 ms Buffer:

5 ms
5 ms
12 ms
5 ms
5 ms
Result:

Microstutter absorbed within the temporal cushion.
The variance still exists internally.

The user simply does not perceive most of it.

Important Distinction
This hypothesis is not intended to solve:

100 ms shader compilation stalls
200 ms asset streaming stalls
major engine freezes
Those should continue to be addressed through traditional methods.

Instead, this proposal specifically targets:

Residual microstutters
that remain after conventional optimizations.

Why This Idea May Be More Relevant Today
Historically, overall latency budgets were much larger.

Adding extra delay could have been difficult to justify.

Modern systems now operate with:

High-refresh displays
Extremely low system latency
Technologies such as NVIDIA Reflex
Powerful CPUs and GPUs
As a result, sacrificing:

5 ms
10 ms
15 ms
may be a reasonable trade-off if it significantly improves frame-time consistency.

Central Question
Would users prefer:

Scenario A
25 ms
25 ms
25 ms
40 ms
25 ms
25 ms
or:

Scenario B
35 ms
35 ms
35 ms
35 ms
35 ms
35 ms
Scenario B introduces more latency but significantly less variance.

This hypothesis suggests that many users may perceive Scenario B as smoother and more pleasant.

Relationship With Existing Solutions
This proposal is not intended to replace:

Shader precompilation
PSO caching
Asset preloading
Frame pacing optimization
NVIDIA Reflex
Engine-level improvements
Instead, it may complement them.

Ideal workflow:

Large stutters
↓
Prevent

Residual microstutters
↓
Absorb
Open Questions
Has this concept already been implemented in commercial engines?

Has any GPU vendor explored similar approaches?

What would be the true latency versus smoothness trade-off?

Could adaptive buffering outperform fixed-size buffering?

Could this coexist with technologies such as NVIDIA Reflex?

What percentage of residual microstutters could realistically be hidden?

Current Status
Conceptual hypothesis.

No implementation currently exists.

Experimental validation is required.

Community feedback and technical discussion are encouraged.

Attribution
Original hypothesis proposed by:

Rodrigo Lagos

This repository serves as the first public publication of this conceptual model.
