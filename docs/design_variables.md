---
title: Design Variables for Design Recovery Control
---

# Design Variables for Design Recovery Control (DRC)

## Purpose

This document defines **what design variables may be modified**  
and **what actions are strictly prohibited**  
within the **Design Recovery Control (DRC)** framework.

This file serves as a **formal job description and boundary contract**  
for any LLM-based design supervision process.

---

## Fundamental Rule

> **The LLM is a design supervisor, not a controller.**

It may **propose or update design assumptions**,  
but it must **never participate in real-time control execution**.

---

## Permitted Design Variables

The LLM may modify **design-level artifacts only**,  
within **explicitly predefined bounds**.

### 1. PID-Related Design Variables

Allowed:

- Gain sets:
  - Proportional gain $K_p$
  - Integral gain $K_i$
  - Derivative gain $K_d$
- Gain scheduling tables (mode-indexed or condition-indexed)
- Valid operating ranges for each gain

Constraints:

- Gains must remain within predefined numerical bounds
- Controller structure (PID form) must not be altered
- Sampling period and execution timing are immutable

Not allowed:

- Injecting control signals
- Modifying control loop execution order
- Introducing adaptive or self-learning PID logic

---

### 2. FSM-Related Design Variables

Allowed:

- State transition conditions
- Threshold values used in guards
- Timeout parameters
- State annotations and descriptions
- Mode classification logic

Constraints:

- FSM topology must remain intact unless explicitly approved
- Safety-critical states must not be bypassed
- Transition logic must remain deterministic

Not allowed:

- Removing safety states
- Adding hidden or implicit transitions
- Allowing uncontrolled state jumps

---

### 3. Operating Mode Definitions

Allowed:

- Definition of operating modes
- Mode-specific parameter sets
- Entry and exit conditions
- Mode-level constraints and assumptions

Examples:

- Nominal mode
- Degraded mode
- Safe-hold mode
- Diagnostic or inspection mode

Not allowed:

- Modes that directly override PID or FSM authority
- Modes that enable direct actuator access

---

## Explicitly Prohibited Actions

The LLM must never:

- Modify or generate real-time control signals
- Access actuator commands or sensor streams directly
- Alter execution timing, scheduling, or task priority
- Perform continuous online optimization
- Bypass FSM safety guards
- Self-approve deployment of its own design changes

---

## Approval and Deployment Rules

- All LLM-generated design updates must be:
  - Explicit
  - Human-readable
  - Inspectable
  - Reversible

- Deployment may require:
  - Human approval
  - System-level validation
  - Offline simulation or review

- Automatic self-deployment is **not permitted**.

---

## Failure and Degradation Context

Design Recovery Control is activated when:

- Control performance degrades
- Original design assumptions are violated
- Physical systems remain operational
- Safety margins are threatened but not exceeded

DRC does **not** address:

- Physical repair
- Actuator recovery
- Sensor replacement
- Reliability or lifetime optimization

---

## Design Intent Freeze

This document **fixes the scope and authority of design recovery actions**  
within Design Recovery Control.

Future extensions may add **examples or tooling**,  
but **must not expand or relax the permissions or prohibitions defined here**.

---

## Legal and Safety Note

Any implementation violating these constraints  
**must not be labeled as Design Recovery Control (DRC)**.

---

End of document.
