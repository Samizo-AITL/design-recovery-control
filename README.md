# Design Recovery Control

## Overview

**Design Recovery Control (DRC)** is a control architecture that addresses *system degradation*  
by **recovering violated control design assumptions**,  
rather than directly manipulating control inputs or physical systems.

DRC explicitly separates the following layers:

- **Real-time control** — PID  
- **State and safety supervision** — FSM  
- **Design recovery and reconfiguration** — LLM  

The fundamental premise of DRC is:

> **Large Language Models must not replace controllers.**  
> They act solely as *design supervisors* when original control assumptions no longer hold.

---

## Motivation

Conventional control frameworks focus primarily on:

- **Reliability Control**  
  → Preventing degradation by reducing physical stress (V–I, temperature, duty cycle)

- **Recovery Control**  
  → Restoring output or function via reset, recalibration, or fallback logic

However, many real-world failures occur because:

> **The original control design assumptions drift or collapse over time**,  
> even when the system remains operational.

**Design Recovery Control targets this gap.**

---

## Core Concept

### Layered Control Structure

```
┌──────────────────────────┐
│ LLM : Design Supervisor  │  ← Design Recovery Control
├──────────────────────────┤
│ FSM : State Management   │
├──────────────────────────┤
│ PID : Real-Time Control  │
├──────────────────────────┤
│ Plant / Physical System  │
└──────────────────────────┘
```

### What Is Recovered — and What Is Not

**DRC does NOT recover:**

- ❌ Control outputs  
- ❌ Control inputs  
- ❌ Physical degradation itself  

**DRC DOES recover:**

- ✅ **Control design assumptions**, including:
  - PID gain validity
  - FSM transition conditions
  - Operating mode definitions

---

## Design Principles

1. **LLM never touches real-time control inputs**
2. **Safety and stability are enforced exclusively by PID and FSM**
3. **LLM operates asynchronously and discontinuously**
4. **All design updates are explicit, inspectable, and reversible**
5. **Human or system-level approval may gate design changes**

---

## Relation to AITL

- **AITL (Adaptive Intelligent Technology Loop)**  
  → An architectural pattern for layered intelligent control systems

- **Design Recovery Control**  
  → A generalized *control engineering concept* defining  
    the role and boundaries of the design supervision layer

This repository formalizes the **design recovery layer** used within AITL-based systems  
as a domain-independent engineering concept.

---

## Typical Use Cases

- Control systems with long-term parameter drift
- Degraded physical systems (thermal, mechanical, semiconductor, MEMS)
- Safety-critical systems where LLM real-time control is unacceptable
- Human-in-the-loop or audit-required control redesign workflows

---

## What This Repository Is NOT

- ❌ An end-to-end LLM controller
- ❌ A reinforcement learning controller
- ❌ A reliability or lifetime optimization framework

---

## Status

This repository focuses on:

- Concept definition
- Architectural clarification
- Minimal, illustrative PoC examples

Domain-specific implementations  
(inkjet, MEMS, semiconductor, robotics, etc.)  
are intentionally handled in separate repositories.

---

## Design Intent Freeze

This document **fixes the conceptual definition of Design Recovery Control**.

Future work may **extend implementations or examples**,  
but **must not redefine the core assumptions or boundaries described here**.

---

## License

MIT License
