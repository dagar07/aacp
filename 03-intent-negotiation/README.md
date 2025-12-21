# Process 3: Intent Negotiation & Permission Granting
*AACP Protocol – Process Specification v1.0*

---

## Overview

**Intent Negotiation & Permission Granting** defines how AI agents explicitly declare, negotiate, validate, and authorize **what action will be performed**, **under which constraints**, and **with what accountability**.

This process ensures that **no AI action is executed implicitly**.

> **Capabilities describe what an AI can do.  
Intent defines what an AI will do.**

---

## Prerequisites

Before entering this process, the following must be completed:

- **Process 1: AI Identity & Registration**
- **Process 2: Capability Discovery**

Required state:
- Valid AI-ID
- Established trust tier
- Discovered and permitted capability descriptors

---

## Purpose

This process exists to:
- Prevent ambiguous or hidden AI behavior
- Make AI actions explicit, inspectable, and auditable
- Allow safe negotiation between autonomous agents
- Bind AI actions to enforceable constraints and policies

---

## Design Principles

1. **Intent must be explicit**
2. **No execution without permission**
3. **Negotiation is bilateral**
4. **Constraints are binding**
5. **Policy overrides autonomy**
6. **Intent is auditable by default**

---

## Intent Model

An **Intent** is a structured declaration of *planned action*.
