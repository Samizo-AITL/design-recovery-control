---
title: "design-recovery-control"
description: "recovering violated control design assumptions"
---

# ❓ FAQ — Design Recovery Control (DRC)

This document addresses **frequent misunderstandings and boundary violations**  
related to **Design Recovery Control (DRC)**.

If a question is not answered here,  
it usually indicates a misunderstanding of the DRC concept itself.

---

## Q1. Is Design Recovery Control a form of AI control?

**No.**

DRC does **not** perform control.

- 🚫 It does not generate control inputs  
- 🚫 It does not replace controllers  
- 🚫 It does not execute in real time  

DRC supervises **control design assumptions only**.

---

## Q2. Does the LLM control the system in DRC?

**Absolutely not.**

In DRC:

- ⏱ **PID** controls the system  
- 🔄 **FSM** enforces safety and state logic  
- 🧠 **LLM** operates **offline and asynchronously**  

Any system where an LLM directly influences actuator commands  
**is not DRC**.

---

## Q3. Is DRC similar to adaptive control?

**No.**

Adaptive control:
- modifies control behavior **online**
- adapts continuously to observed dynamics

DRC:
- ❌ does not adapt online  
- ❌ does not self-learn  
- ❌ does not autonomously modify controllers  

DRC updates **design artifacts**, not execution logic.

---

## Q4. Is DRC a type of reinforcement learning?

**No.**

| Aspect | DRC | RL |
|------|-----|----|
| Learns policies | ❌ | ✅ |
| Optimizes rewards | ❌ | ✅ |
| Outputs actions | ❌ | ✅ |

The two approaches are **conceptually incompatible**.

---

## Q5. Can DRC fix hardware failures?

**No.**

DRC does not address:

- actuator failure  
- sensor failure  
- structural damage  
- electrical faults  

These are handled by **maintenance, redundancy, or fault isolation**.

---

## Q6. When is DRC activated?

DRC is activated when:

- 📉 control performance degrades  
- 📐 design assumptions no longer hold  
- ⚙ the system remains operational  
- 🛡 safety margins are still intact  

DRC is **not** an emergency response mechanism.

---

## Q7. Can DRC run continuously in the background?

**No.**

DRC is:

- 🔔 event-driven or periodically invoked  
- ⏱ discrete and non-continuous  
- 🧭 explicitly triggered  

Continuous or high-frequency invocation  
**violates DRC principles**.

---

## Q8. Does DRC require human approval?

**Often, yes.**

DRC supports:

- 👤 human-in-the-loop review  
- 🧾 audit trails  
- 🔐 approval gating  

🚫 Fully autonomous self-deployment is **not permitted**.

---

## Q9. Can DRC change the structure of the controller or FSM?

**No — unless explicitly approved outside the DRC process.**

By default:

- controller structure is fixed  
- FSM topology is fixed  
- only parameters and assumptions may change  

Structural redesign is **out of scope** for DRC.

---

## Q10. Is DRC suitable for safety-critical systems?

**Yes — by design.**

DRC was created to:

- 🛡 preserve deterministic control  
- 🔍 maintain inspectability  
- 📜 support certification workflows  

It avoids the risks of real-time AI control.

---

## Q11. Can DRC be combined with RL or AI control?

**Not at the same control layer.**

- RL or AI control may exist elsewhere  
- DRC must not supervise AI controllers  
- 🔒 layer boundaries must remain strict  

Mixing control authority **invalidates DRC**.

---

## Q12. Why use an LLM at all in DRC?

Because:

- design assumptions are expressed in language  
- long-term degradation is context-rich  
- human-like design reasoning is required  
- outputs must be inspectable and explainable  

The LLM replaces **design review effort**,  
not control execution.

---

## Q13. Is DRC domain-specific?

**No.**

DRC is domain-independent and applies to:

- mechanical systems  
- thermal systems  
- semiconductor processes  
- MEMS  
- robotics  

Domain-specific implementations belong in **separate repositories**.

---

## Q14. Can DRC modify safety limits?

**No.**

- safety limits are enforced by FSM and hardware interlocks  
- DRC may **propose** revised assumptions  
- DRC must **never override** safety constraints  

---

## Q15. What invalidates a claim of DRC?

Any system that:

- allows LLMs to control actuators  
- performs online self-learning control  
- bypasses FSM safety logic  
- blurs design and execution layers  

**must not be described as Design Recovery Control.**

---

## 🔒 Design Intent Freeze

This FAQ **fixes the interpretation boundaries**  
of Design Recovery Control.

Future clarifications may be added,  
but **must not weaken or expand the authority defined here**.

---

*End of document.*
