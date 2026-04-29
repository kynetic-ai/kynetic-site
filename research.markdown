---
layout: page
title: Research
permalink: /research/
---

## The Architecture Question

Kynetic's research is organized around a central question: **can a hierarchical architecture with a learned embedding interface achieve better sim-to-real transfer than direct action prediction?**

### Core Research Areas

**Hierarchical Robot Learning**
How should a robot intelligence be structured? We're investigating architectures that separate high-level task reasoning from low-level motor control, connected through a learned embedding space. This draws on work in hierarchical reinforcement learning, representation learning, and sim-to-real transfer.

**Embodiment-Agnostic Representations**
What makes a representation of movement "embodied" — and can we make it abstract enough to transfer? Our embedding space is designed to capture the semantics of motion independent of any specific robot's kinematics or dynamics.

**Sim-to-Real Transfer**
Training in simulation, deploying in reality. We're developing protocols to close the sim-to-real gap without requiring millions of real-world episodes. The hierarchical architecture may help: when only the low-level controller needs to bridge the gap, the transfer problem becomes more tractable.

**Human-in-the-Loop Fine-Tuning**
Human demonstration data is scarce and expensive. We're building pipelines that make efficient use of demonstrations — via accessible consumer hardware — to fine-tune policies pre-trained in simulation.

### Methodology

We're methodology-agnostic. That means:

- No commitment to specific network architectures
- No single simulator or training framework
- Decisions driven by experimental evidence, not prior beliefs
- Open to incorporating the best ideas from the broader research community

### Publications & Updates

Research outputs, experiment results, and technical notes will appear on this page and the blog as the work progresses.
