---
title: Frequently Asked Questions (FAQ)
---

# FAQ — Design Recovery Control (DRC)

This document addresses **frequent misunderstandings and boundary violations**  
related to Design Recovery Control (DRC).

If a question is not answered here,  
it likely indicates a misunderstanding of the DRC concept.

---

## Q1. Is Design Recovery Control a form of AI control?

**No.**

DRC does **not** perform control.

- It does not generate control inputs
- It does not replace controllers
- It does not execute in real time

DRC supervises **control design assumptions only**.

---

## Q2. Does the LLM control the system in DRC?

**Absolutely not.**

In DRC:

- PID controls the system
- FSM enforces safety and state logic
- LLM operates **offline and asynchronously**

Any system where an LLM directly influences actuator commands  
**is not DRC**.

---

## Q3. Is DRC similar to adaptive control?

**No.**

Adaptive control modifies control behavior **online**  
based on observed dynamics.

DRC:

- Does not adapt online
- Does not self-learn
- Does not modify controllers autonomously

DRC updates **design artifacts**, not execution logic.

---

## Q4. Is DRC a type of reinforcement learning?

**No.**

Reinforcement learning:

- Learns policies
- Optimizes reward functions
- Directly outputs actions

DRC:

- Does not learn policies
- Does not optimize rewards
- Does not output actions

The two approaches are **conceptually incompatible**.

---

## Q5. Can DRC fix hardware failures?

**No.**

DRC does not address:

- Actuator failure
- Sensor failure
- Structural damage
- Electrical faults

These are handled by maintenance, redundancy, or fault isolation.

---

## Q6. When is DRC activated?

DRC is activated when:

- Control performance degrades
- Design assumptions no longer hold
- The system remains operational
- Safety margins are still intact

DRC is **not** an emergency response mechanism.

---

## Q7. Can DRC run continuously in the background?

**No.**

DRC is:

- Event-driven or periodically invoked
- Discrete and non-continuous
- Explicitly triggered

Continuous or high-frequency invocation  
violates DRC principles.

---

## Q8. Does DRC require human approval?

**Often, yes.**

DRC supports:

- Human-in-the-loop review
- Audit trails
- Approval gating

Fully autonomous self-deployment  
is **not permitted** by design.

---

## Q9. Can DRC change the structure of the controller or FSM?

**No, unless explicitly approved outside the DRC process.**

By default:

- Controller structure is fixed
- FSM topology is fixed
- Only parameters and assumptions may change

Structural redesign is **out of scope** for DRC.

---

## Q10. Is DRC suitable for safety-critical systems?

**Yes — by design.**

DRC was explicitly created to:

- Preserve deterministic control
- Maintain inspectability
- Enable certification workflows

It avoids the risks of real-time AI control.

---

## Q11. Can DRC be combined with RL or AI control?

**Not at the same control layer.**

- RL or AI control may exist in separate systems
- DRC must not supervise AI controllers
- Layer boundaries must remain strict

Mixing control authority invalidates DRC.

---

## Q12. Why use an LLM at all in DRC?

Because:

- Design assumptions are expressed in language
- Long-term degradation is context-rich
- Human-like design reasoning is required
- Outputs must be inspectable and explainable

The LLM replaces **design review effort**,  
not control execution.

---

## Q13. Is DRC domain-specific?

**No.**

DRC is domain-independent.

It applies to:

- Mechanical systems
- Thermal systems
- Semiconductor processes
- MEMS
- Robotics

Domain-specific implementations belong elsewhere.

---

## Q14. Can DRC modify safety limits?

**No.**

Safety limits are enforced by FSM and hardware interlocks.

DRC may **propose** revised assumptions,  
but must not override safety constraints.

---

## Q15. What invalidates a claim of DRC?

Any system that:

- Allows LLMs to control actuators
- Performs online self-learning control
- Bypasses FSM safety logic
- Blurs design and execution layers

**must not be described as Design Recovery Control.**

---

## Design Intent Freeze

This FAQ **fixes the interpretation boundaries**  
of Design Recovery Control.

Future clarifications may be added,  
but **must not weaken or expand the authority defined here**.

---

End of document.
