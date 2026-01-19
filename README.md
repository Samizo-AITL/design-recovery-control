# 🛠 Design Recovery Control

## 📌 Overview

**Design Recovery Control (DRC)** is a control architecture that addresses *system degradation*  
by **recovering violated control design assumptions**,  
rather than directly manipulating control inputs or physical systems.

DRC explicitly separates the following layers:

- ⏱ **Real-time control** — PID  
- 🔄 **State and safety supervision** — FSM  
- 🧠 **Design recovery and reconfiguration** — LLM  

The fundamental premise of DRC is:

> **Large Language Models must not replace controllers.**  
> They operate strictly as *design supervisors* when original control assumptions no longer hold.

---

## 🎯 Motivation

Conventional control frameworks focus primarily on:

- 🛡 **Reliability Control**  
  → Preventing degradation by reducing physical stress (V–I, temperature, duty cycle)

- 🔁 **Recovery Control**  
  → Restoring output or function via reset, recalibration, or fallback logic

However, many real-world failures occur because:

> **The original control design assumptions drift or collapse over time**,  
> even when the system remains operational.

➡️ **Design Recovery Control explicitly targets this gap.**

---

## 🧠 Core Concept

### 🧩 Layered Control Structure

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

### 🔍 What Is Recovered — and What Is Not

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

## 📐 Scope of Design Recovery

The LLM is permitted to modify **design-level artifacts only**, including:

- 🧮 PID gain sets *(Kp, Ki, Kd)* **within predefined bounds**
- 🔄 FSM transition conditions and thresholds
- 🗺 Operating mode definitions and annotations

The LLM is **explicitly prohibited** from:

- 🚫 Injecting or modifying control signals
- 🚫 Accessing real-time control loops
- 🚫 Altering execution timing or scheduling
- 🚫 Bypassing FSM safety guards
- 🚫 Performing continuous or autonomous online control

All LLM-generated changes must be **explicit, inspectable, and reversible**,  
and may require **human or system-level approval** before deployment.

---

## 📜 Design Principles

1. 🔒 **LLM never touches real-time control inputs**
2. 🛡 **Safety and stability are enforced exclusively by PID and FSM**
3. ⏳ **LLM operates asynchronously and discontinuously**
4. 🔍 **All design updates are explicit, inspectable, and reversible**
5. 👤 **Human or system-level approval may gate design changes**

---

## 🔗 Relation to AITL

- 🧠 **AITL (Adaptive Intelligent Technology Loop)**  
  → An architectural pattern for layered intelligent control systems

- 🛠 **Design Recovery Control**  
  → A domain-independent *control engineering concept*  
    defining the role and boundaries of the design supervision layer

This repository **formalizes the design recovery layer**  
used within AITL-based systems,  
without binding it to any specific application domain.

---

## 🛠 Typical Use Cases

- ⏳ Control systems with long-term parameter drift
- 🧱 Degraded physical systems (thermal, mechanical, semiconductor, MEMS)
- 🚨 Safety-critical systems where LLM real-time control is unacceptable
- 👥 Human-in-the-loop or audit-required control redesign workflows

---

## 🚫 What This Repository Is NOT

- ❌ An end-to-end LLM controller
- ❌ A reinforcement learning controller
- ❌ A reliability or lifetime optimization framework

---

## 📦 Repository Scope

This repository focuses on:

- 📘 Concept definition
- 🧩 Architectural clarification
- 📐 Boundary and responsibility specification
- 🧪 Minimal, illustrative PoC references (non-real-time)

Domain-specific implementations  
(inkjet, MEMS, semiconductor, robotics, etc.)  
are intentionally handled in **separate repositories**.

---

## 📚 Documentation

- 📘 [Design Variables](docs/design_variables.md)
- 🔄 [Design Recovery Workflow](docs/recovery_workflow.md)
- ⚠ [Failure Modes](docs/failure_modes.md)
- 📊 [Comparison: DRC vs RL vs LLM Control](docs/comparison_rl_llm_control.md)
- ❓ [FAQ](docs/faq.md)
- 🧾 [Audit Checklist](docs/audit_checklist.md)
- 🧠 [LLM Prompt Template](docs/llm_prompt_template.md)

---

## 🧪 Proof of Concept (PoC)

- 🧩 [Minimal Design Proposal PoC (Python)](poc/drc_design_proposal.py)

---

## 🔒 Design Intent Freeze

This document **fixes the conceptual definition of Design Recovery Control**.

Future work may **extend implementations or examples**,  
but **must not redefine the core assumptions, boundaries, or prohibitions described here**.

---

## Author

| 📌 Item | Details |
|--------|---------|
| **Name** | Shinichi Samizo |
| **Expertise** | Semiconductor devices (logic, memory, high-voltage mixed-signal)<br>Thin-film piezo actuators for inkjet systems<br>PrecisionCore printhead productization, BOM management, ISO training |
| **GitHub** | [![GitHub](https://img.shields.io/badge/GitHub-Samizo--AITL-black?logo=github)](https://github.com/Samizo-AITL) |

---

## License

[![Hybrid License](https://img.shields.io/badge/license-Hybrid-blueviolet)](https://samizo-aitl.github.io/design-recovery-control/#---license)

| 📌 Item | License | Description |
|--------|---------|-------------|
| **Source Code** | [**MIT License**](https://opensource.org/licenses/MIT) | Free to use, modify, and redistribute |
| **Text Materials** | [**CC BY 4.0**](https://creativecommons.org/licenses/by/4.0/) or [**CC BY-SA 4.0**](https://creativecommons.org/licenses/by-sa/4.0/) | Attribution required; share-alike applies for BY-SA |
| **Figures & Diagrams** | [**CC BY-NC 4.0**](https://creativecommons.org/licenses/by-nc/4.0/) | Non-commercial use only |
| **External References** | Follow the original license | Cite the original source properly |

---

## Feedback

> Suggestions, improvements, and discussions are welcome via GitHub Discussions.

[![💬 GitHub Discussions](https://img.shields.io/badge/💬%20GitHub-Discussions-brightgreen?logo=github)](https://github.com/Samizo-AITL/design-recovery-control/discussions)

