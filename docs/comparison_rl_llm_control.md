---
title: "design-recovery-control"
description: "recovering violated control design assumptions"
---

# 📊 Comparison  
## Design Recovery Control vs RL-Based Control vs LLM-Based Control

---

## 🎯 Purpose

This document provides a **strict, explicit, and non-negotiable comparison** between:

- 🛠 **Design Recovery Control (DRC)**
- 🔁 **Reinforcement Learning (RL)–based control**
- 🧠 **LLM-based control systems**

Its purpose is to **prevent conceptual mixing**,  
especially in **safety-critical, audited, or certified engineering contexts**.

---

## 🔑 Fundamental Conceptual Difference

> **The decisive difference is *what is being controlled*.**

| Framework | What Is Directly Controlled |
|---------|-----------------------------|
| 🛠 **DRC** | **Control design assumptions** |
| 🔁 RL-based control | Control inputs or learned policies |
| 🧠 LLM-based control | Control decisions or actions |

This distinction is architectural, not stylistic.

---

## 🧩 Architectural Comparison

| Aspect | 🛠 DRC | 🔁 RL-Based Control | 🧠 LLM-Based Control |
|------|-------|--------------------|--------------------|
| Real-time control | PID / FSM only | Learned policy | LLM inference |
| Learning element | None | Central | Central |
| LLM role | Design supervisor only | None | Primary controller |
| Execution timing | Asynchronous, discrete | Continuous / online | Continuous or event-driven |
| Safety authority | PID + FSM (explicit) | External or learned | Often implicit |
| Determinism | Deterministic | Often stochastic | Non-deterministic |
| Inspectability | Full | Partial | Low |
| Certification suitability | **High** | Low–Medium | **Very low** |

---

## 🔒 Control Authority Boundary

### 🛠 Design Recovery Control (DRC)

- The LLM **never** touches:
  - control inputs,
  - actuator commands,
  - real-time execution paths.

- The LLM **only** modifies:
  - design parameters,
  - design assumptions,
  - configuration artifacts.

👉 **Control authority remains fully classical and deterministic.**

---

### 🔁 Reinforcement Learning–Based Control

- Learned policy directly outputs control actions
- Control logic is implicit and learned
- Safety is typically enforced via constraints or wrappers

⚠ Common risks:
- policy opacity,
- distribution shift sensitivity,
- certification difficulty.

---

### 🧠 LLM-Based Control

- LLM reasons about commands or actions
- Real-time guarantees are weak or absent
- Output variability is intrinsic

⚠ Common risks:
- non-deterministic behavior,
- hallucination under uncertainty,
- incompatibility with hard safety constraints.

---

## 🔄 Learning vs Recovery

| Concept | 🛠 DRC | 🔁 RL | 🧠 LLM Control |
|-------|-------|------|---------------|
| Online learning | ❌ No | ✅ Yes | ⚠ Sometimes |
| Self-modifying behavior | ❌ No | ✅ Yes | ❌ Often |
| Design intent preservation | ✅ Yes | ❌ No | ❌ No |
| Assumption recovery | ✅ Yes | ❌ No | ❌ No |

DRC restores **design validity**,  
not behavior.

---

## ⚠ Failure Handling Philosophy

### 🛠 DRC

- Assumes:
  - the physical system remains operational,
  - the control structure is still meaningful.
- Repairs:
  - violated **design assumptions**.

---

### 🔁 RL / 🧠 LLM Control

- Attempts to:
  - adapt behavior directly,
  - learn new control policies.

🚫 These philosophies are **fundamentally irreconcilable**.

---

## 🛡 Safety and Certification Perspective

| Criterion | 🛠 DRC | 🔁 RL | 🧠 LLM Control |
|---------|-------|------|---------------|
| Real-time determinism | ✅ | ❌ | ❌ |
| Explicit safety guards | ✅ FSM | ⚠ Optional | ❌ Rare |
| Auditability | ✅ | ⚠ Partial | ❌ |
| Formal verification | ✅ | ❌ | ❌ |
| Human approval gating | ✅ | ❌ | ❌ |

---

## 🧭 When Each Approach Is Appropriate

### Use 🛠 DRC when:
- safety certification is required,
- long-term degradation occurs,
- human review is mandatory,
- design intent must be preserved.

---

### Use 🔁 RL when:
- the environment is well-bounded,
- exploration is acceptable,
- safety risk is low or externally mitigated.

---

### Use 🧠 LLM-Based Control when:
- the system is non-critical,
- high-level autonomy is desired,
- failure consequences are minimal.

---

## 🚫 Explicit Non-Equivalence Statement

> **Design Recovery Control is NOT a form of reinforcement learning.**  
> **Design Recovery Control is NOT an LLM-based controller.**

Any system that allows an RL agent or LLM  
to directly influence control inputs  
**must not be described as DRC**.

---

## 🔒 Design Intent Freeze

This document **fixes the conceptual boundaries**  
between DRC, RL-based control, and LLM-based control.

Future documents may expand examples,  
but **must not blur, merge, or reinterpret these categories**.

---

*End of document.*
