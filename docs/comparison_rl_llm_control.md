---
title: Comparison of DRC, RL-Based Control, and LLM-Based Control
---

# Comparison of Design Recovery Control, RL-Based Control, and LLM-Based Control

## Purpose

This document provides a **strict and unambiguous comparison** between:

- **Design Recovery Control (DRC)**
- **Reinforcement Learning (RL)-based control**
- **LLM-based control systems**

The goal is to **prevent conceptual mixing**,  
especially in safety-critical or engineering-reviewed contexts.

---

## Fundamental Conceptual Difference

> **The key difference is *what is being controlled*.**

| Framework | What It Directly Controls |
|---------|---------------------------|
| DRC | **Control design assumptions** |
| RL-based control | Control inputs or policies |
| LLM-based control | Control decisions or actions |

---

## Architectural Comparison

| Aspect | DRC | RL-Based Control | LLM-Based Control |
|------|-----|-----------------|------------------|
| Real-time control | PID / FSM only | Learned policy | LLM inference |
| LLM role | Design supervisor only | None | Primary controller |
| Execution timing | Asynchronous, discrete | Continuous / online | Continuous or event-driven |
| Safety authority | PID + FSM | External or learned | Often implicit |
| Determinism | Deterministic control | Often stochastic | Non-deterministic |
| Inspectability | Full | Partial | Low |
| Certification suitability | High | Low–Medium | Very low |

---

## Control Authority Boundary

### Design Recovery Control (DRC)

- LLM **never** touches:
  - Control inputs
  - Actuator commands
  - Real-time execution

- LLM **only** modifies:
  - Design parameters
  - Assumptions
  - Configuration artifacts

👉 Control authority remains **fully classical**.

---

### Reinforcement Learning–Based Control

- Policy directly outputs control actions
- Control logic is learned, not explicitly designed
- Safety often handled via constraints or wrappers

Risks:

- Policy opacity
- Distribution shift sensitivity
- Certification difficulty

---

### LLM-Based Control

- LLM reasons about actions or commands
- Often lacks strict real-time guarantees
- Output variability is intrinsic

Risks:

- Non-deterministic behavior
- Hallucination under uncertainty
- Incompatible with hard safety constraints

---

## Learning vs Recovery

| Concept | DRC | RL | LLM Control |
|-------|-----|----|-------------|
| Online learning | ❌ No | ✅ Yes | Sometimes |
| Self-modifying behavior | ❌ No | ✅ Yes | Often |
| Design intent preservation | ✅ Yes | ❌ No | ❌ No |
| Assumption recovery | ✅ Yes | ❌ No | ❌ No |

---

## Failure Handling Philosophy

### DRC

- Assumes:
  - Physical system still operational
  - Control logic still valid
- Fixes:
  - Broken design assumptions

### RL / LLM Control

- Often attempts to:
  - Adapt behavior directly
  - Learn new control policies

This difference is **fundamental and irreconcilable**.

---

## Safety and Certification Perspective

| Criterion | DRC | RL | LLM Control |
|---------|-----|----|-------------|
| Real-time determinism | ✅ | ❌ | ❌ |
| Explicit safety guards | ✅ FSM | ⚠ Optional | ❌ Rare |
| Auditability | ✅ | ⚠ Partial | ❌ |
| Formal verification | ✅ | ❌ | ❌ |
| Human approval gating | ✅ | ❌ | ❌ |

---

## When Each Approach Is Appropriate

### Use DRC when:

- Safety certification is required
- Long-term degradation occurs
- Human review is mandatory
- Design intent must be preserved

### Use RL when:

- Environment is well-bounded
- Exploration is acceptable
- Safety risk is low or mitigated

### Use LLM Control when:

- System is non-critical
- High-level autonomy is desired
- Failure consequences are minimal

---

## Explicit Non-Equivalence Statement

> **Design Recovery Control is NOT a form of reinforcement learning.**  
> **Design Recovery Control is NOT an LLM-based controller.**

Any system that allows an LLM or RL agent  
to directly influence control inputs  
**must not be described as DRC**.

---

## Design Intent Freeze

This comparison **fixes the conceptual boundaries**  
between DRC, RL-based control, and LLM-based control.

Future documents may expand examples,  
but **must not blur or merge these categories**.

---

End of document.
