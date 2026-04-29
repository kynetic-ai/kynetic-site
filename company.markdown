---
layout: page
title: Company
permalink: /company/
---

## Our Approach

Kynetic Intelligence is built on a simple thesis: **robot intelligence should not be tied to a single body.**

Today's robots are one-offs. A controller built for a warehouse arm doesn't work on a humanoid. A humanoid policy doesn't transfer to a quadruped. Every new robot requires a new stack. This is the bottleneck.

Our architecture separates task reasoning from physical execution. A high-level policy decides *what to do*. A low-level controller handles *how to move*. Between them is a learned embedding space — a shared language of movement and intent. This means:

- **Embodiment-agnostic high-level reasoning.** One policy. Multiple robots.
- **Grounded low-level control.** Real physics. Contact-rich dynamics. Real transfer.
- **Composable skills.** Behaviors learned in simulation combine into novel sequences.

We're methodology-agnostic — not committed to any specific neural network architecture, training algorithm, simulator, or hardware platform. The architecture is the bet.

## Training Pipeline

Our three-stage pipeline is designed for data efficiency and sim-to-real transfer:

1. **Pre-training** — Diverse simulated tasks across embodiments build broad capabilities
2. **Supervised fine-tuning** — Human demonstration data via accessible consumer hardware
3. **RL fine-tuning** — Task-specific reinforcement learning on target objectives

## Founder

**Miguel Alonso Jr.** is the founder and CEO of Kynetic Intelligence.

- PhD in Electrical and Computer Engineering, NSF Graduate Research Fellow
- Former lead of ML-Agents at Unity Technologies
- Visiting Associate Professor at Florida International University
- $1M+ in secured research funding
- Developed full-body teleoperation and sim-to-real systems for humanoid and bi-manual robots

## Status

We are in the **simulation phase** — building infrastructure, training pipelines, and evaluation protocols. Hardware is on a 12-month horizon. Our core research question: can a hierarchical architecture with a learned embedding interface achieve better sim-to-real transfer than direct action prediction?

## Contact

[GitHub](https://github.com/kynetic-ai) &middot; miguel@kynetic.ai
