---
title: "design-recovery-control"
description: "recovering violated control design assumptions"
---

# 📐 Design Variables for Design Recovery Control (DRC)

## 🎯 Purpose

This document defines **which design variables may be modified**  
and **which actions are strictly prohibited**  
within the **Design Recovery Control (DRC)** framework.

This file serves as a **formal boundary contract and job description**  
for any **LLM-based design supervision process**.

Failure to comply with this document  
**invalidates any claim of DRC compliance**.

---

## 🔑 Fundamental Rule

> **The LLM is a design supervisor, not a controller.**

The LLM may **propose or update control design assumptions**,  
but must **never participate in real-time control execution**.

This rule is absolute and non-negotiable.

---

## ✅ Permitted Design Variables

The LLM may modify **design-level artifacts only**,  
and **only within explicitly predefined bounds**.

---

### 🎚 1. PID-Related Design Variables

#### Allowed

- Gain sets:
  - Proportional gain $K_p$
  - Integral gain $K_i$
  - Derivative gain $K_d$
- Gain scheduling tables  
  *(mode-indexed or condition-indexed)*
- Valid operating ranges for each gain

#### Constraints

- Gains must remain within predefined numerical bounds
- Controller structure (**PID form**) must not be altered
- Sampling period and execution timing are **immutable**

#### Not Allowed

- 🚫 Injecting or modifying control signals
- 🚫 Changing control loop execution order
- 🚫 Introducing adaptive, learning, or self-tuning PID logic

---

### 🔄 2. FSM-Related Design Variables

#### Allowed

- State transition conditions
- Guard threshold values
- Timeout and persistence parameters
- State annotations and semantic descriptions
- Mode classification logic

#### Constraints

- FSM topology is immutable unless **explicitly approved**
- Safety-critical states must never be bypassed
- Transition logic must remain **deterministic**

#### Not Allowed

- 🚫 Removing or disabling safety states
- 🚫 Adding hidden, implicit, or undocumented transitions
- 🚫 Allowing uncontrolled or non-deterministic state jumps

---

### 🗺 3. Operating Mode Definitions

#### Allowed

- Definition and naming of operating modes
- Mode-specific parameter sets
- Entry and exit conditions
- Mode-level constraints and assumptions

#### Examples

- Nominal mode  
- Degraded mode  
- Safe-hold mode  
- Diagnostic or inspection mode  

#### Not Allowed

- 🚫 Modes that override PID or FSM authority
- 🚫 Modes that enable direct actuator access
- 🚫 Modes that weaken envelope or safety constraints

---

## 🚫 Explicitly Prohibited Actions

Under no circumstances may the LLM:

- Modify or generate real-time control signals
- Access actuator commands or live sensor streams
- Alter execution timing, scheduling, or task priority
- Perform continuous or autonomous online optimization
- Bypass or weaken FSM safety guards
- Self-approve or auto-deploy its own design changes

Violation of any item above constitutes **immediate non-compliance**.

---

## 🧑‍⚖️ Approval and Deployment Rules

All LLM-generated design updates must be:

- 📄 Explicit
- 👁 Human-readable
- 🔍 Inspectable
- 🔁 Reversible

Deployment may require one or more of the following:

- 👤 Human approval
- ⚙ System-level validation
- 🧪 Offline simulation or review

🚫 **Automatic self-deployment is strictly prohibited.**

---

## ⚠ Failure and Degradation Context

Design Recovery Control is activated when:

- Control performance degrades
- Original design assumptions are violated
- Physical systems remain operational
- Safety margins are threatened but not yet exceeded

DRC explicitly does **not** address:

- Physical repair or replacement
- Actuator recovery
- Sensor replacement or recalibration
- Reliability, lifetime, or wear optimization

These concerns belong to **other architectural layers**.

---

## 🔒 Design Intent Freeze

This document **fixes the scope, authority, and limits**  
of design recovery actions within Design Recovery Control.

Future work may add **examples, tooling, or templates**,  
but **must not expand, relax, or reinterpret**  
the permissions or prohibitions defined here.

---

## ⚖ Legal and Safety Notice

Any implementation that violates this document  
**must not be labeled or represented as  
Design Recovery Control (DRC)**.

---

*End of document.*
