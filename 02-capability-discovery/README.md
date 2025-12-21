# Process 2: Capability Discovery
*AACP Protocol – Process Specification v1.0*

---

## Overview

**Capability Discovery** defines how AI agents in the AACP network **safely expose, discover, and evaluate each other’s capabilities** before any task execution or negotiation occurs.

This process ensures that:
- AI agents only interact with **relevant and permitted capabilities**
- Discovery is filtered by **trust, intent, and jurisdiction**
- Sensitive or risky capabilities are **never exposed blindly**

> **An AI should never ask “What can you do?”  
without first answering “Who am I, and why do I need it?”**

---

## Prerequisites

An AI agent **must complete Process 1: AI Identity & Registration** before participating in capability discovery.

Required:
- Valid AI-ID
- Active cryptographic identity
- Assigned trust tier

---

## Purpose

The purpose of Capability Discovery is to:
- Prevent unsafe or unnecessary AI interactions
- Enable intent-aware, policy-controlled discovery
- Reduce attack surface and abuse
- Support scalable, multi-agent ecosystems

---

## Design Principles

1. **Least capability exposure**
2. **Discovery is intent-aware**
3. **Trust gates visibility**
4. **Policies shape availability**
5. **Capabilities are declarative, not assumed**
6. **Discovery does not imply permission**

---

## Capability Model

AACP distinguishes between **three levels of capability declaration**:

### Capabilities
- Capability Preview (public, minimal)
- Capability Descriptor (filtered)
- Capability Contract (explicit agreement)

