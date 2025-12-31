# Design Recovery Control

## Overview

**Design Recovery Control (DRC)** is a control architecture that addresses *system degradation*  
by **recovering control design assumptions**, rather than directly manipulating control inputs.

This framework explicitly separates:

- **Real-time control** (PID)
- **State supervision** (FSM)
- **Design recovery and reconfiguration** (LLM)

The key idea is that **LLMs should not replace controllers**,  
but instead act as *design supervisors* when the original control assumptions are no longer valid.

---

## Motivation

Traditional control approaches focus on:

- **Reliability Control**  
  → preventing degradation by reducing stress (V–I, temperature, duty)

- **Recovery Control**  
  → restoring outputs via reset, recalibration, or fallback control

However, many real systems fail because **the original control design assumptions drift over time**.

Design Recovery Control targets this gap.

---

## Core Concept

### Control Layers

```
┌──────────────────────────┐
│ LLM : Design Supervisor  │  ← Design Recovery
├──────────────────────────┤
│ FSM : State Management   │
├──────────────────────────┤
│ PID : Real-Time Control  │
├──────────────────────────┤
│ Plant / Physical System  │
└──────────────────────────┘
```

### What is Recovered?

- ❌ Control output
- ❌ Control input
- ❌ Physical degradation itself

- ✅ **Control design assumptions**
  - PID gains
  - FSM transition rules
  - Operating mode definitions

---

## Design Principles

1. **LLM never touches real-time control inputs**
2. **Safety is enforced by FSM and PID**
3. **LLM operates asynchronously and discontinuously**
4. **Design updates are explicit, inspectable, and reversible**

---

## Relation to AITL

- **AITL (Adaptive Intelligent Technology Loop)**  
  → Architecture pattern

- **Design Recovery Control**  
  → Control category / engineering concept

This repository provides the *generalized and formalized definition* of the design recovery layer used in AITL-based systems.

---

## Typical Use Cases

- Control systems with long-term parameter drift
- Degraded physical systems (thermal, mechanical, semiconductor, MEMS)
- Safety-critical systems where LLM real-time control is unacceptable
- Human-in-the-loop or audit-required control redesign

---

## What This Repository Is NOT

- ❌ An end-to-end LLM controller
- ❌ A reinforcement learning controller
- ❌ A reliability or lifetime optimization framework

---

## Status

This repository focuses on **concept definition, architecture, and minimal PoC examples**.  
Domain-specific implementations (inkjet, MEMS, semiconductor, robotics) are handled in separate repositories.

---

## License

MIT License
