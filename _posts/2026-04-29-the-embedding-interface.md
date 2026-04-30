---
layout: post
title: "The Embedding Interface"
date: 2026-04-29 21:45:00 -0500
categories: research
---

Everyone building robot foundation models is asking the same question: what's the right architecture?

The naive answer is "train one big model on everything." Pour every robot dataset you can find into a transformer, cross your fingers, and hope the model figures out that a Unitree H1 and a Franka arm have different joint configurations.

That's not a real answer. It's a bet — and an expensive one — that data volume solves the embodiment problem. Maybe it does. But I think the architecture question is more interesting, and the answer matters more than the dataset size.

## The Two-Level Problem

Robot control decomposes naturally into two levels:

**High-level:** What should the robot do? Pick up the mug. Open the drawer. Navigate to the charging station. This is about intent, task structure, and semantic understanding of the world.

**Low-level:** How should the robot move? Joint torques, contact forces, impedance parameters, end-effector trajectories. This is about physics, embodiment geometry, and real-time control.

The question isn't *whether* to separate these levels. Most serious efforts do, in some form. The question is: **what passes between them — and how does it get there?**

In our architecture, the answer has three pieces: a VLA that produces intent, a learned mapping that translates intent into skill embeddings, and a low-level controller that decodes those embeddings into action. The key insight lives in the middle — the embedding space itself.

## The Direct Approach

Skild AI has built an impressive system — $1.8 billion in funding, a team out of CMU, and a hierarchical architecture they call the Skild Brain. Their high-level policy passes commands directly to the low-level policy. "Move the end effector to position X with stiffness Y." Concrete, explicit, interpretable.

This works. It's the straightforward way to chain two policies. But it's also a tight coupling: every new embodiment needs the high-level policy to understand its specific control interface. The abstraction leaks.

## The Embedding Approach

We take a different bet.

Instead of passing explicit commands between levels, we pass through a learned embedding space — a compressed, structured representation of *how to move* rather than *where to move*. The high-level policy (a VLA) produces task-goal intent. That intent maps through to a skill embedding — a point in a shared latent space that captures motor-primitive structure. The low-level controller — embodiment-specific, trained per platform — decodes that embedding into control.

This sounds abstract. Here's what it means in practice:

The same embedding that corresponds to "reach toward object" compiles to different joint trajectories on a humanoid arm versus a 7-DOF manipulator versus a wheeled base with a gripper. Intent comes from the VLA — the embedding translates it into movement structure. Each low-level controller knows how to realize that structure on its hardware.

## Why This Matters

Three reasons:

**1. Composition.** Embeddings compose. If you have an embedding for "reach" and an embedding for "grasp" and an embedding for "lift," you can sequence them — or even blend them — in embedding space. The interface becomes a language for movement primitives, not a command protocol.

**2. Transfer.** A high-level policy trained on manipulation data produces embeddings that are meaningful for navigation, because the embedding space captures movement structure, not joint configurations. You don't need to retrain the high-level policy every time you add a new robot — you train a new low-level decoder.

**3. Data efficiency.** If the embedding space is well-structured, the high-level policy can learn from diverse embodiment data without the low-level control details interfering. The embedding acts as a bottleneck that forces the policy to represent *what matters* rather than *how to execute*.

## What's Hard

This is not a solved problem. Three things keep me up:

**Learning the embedding space.** You can't hand-design an embedding that captures movement structure across embodiments. It has to be learned. And learning a good one requires training across diverse robots simultaneously — if you train sequentially, the embedding space drifts.

**The sim-to-real gap for embeddings.** It's one thing to get this working in simulation, where you have perfect state and infinite data. It's another to deploy on real hardware where sensor noise, actuator latency, and unmodeled dynamics mean the embedding must be robust to distribution shift.

**Evaluation.** How do you measure whether an embedding space is "good"? Reconstruction loss tells you something. Zero-shot transfer to a new embodiment tells you more. But the real test — does this embedding make it easier to learn new tasks? — is expensive and noisy.

## The State of Play

The robot learning field is moving fast. Physical Intelligence has shown remarkable results with π₀, their VLA model. Skild has the scale and the team. Figure is shipping humanoids.

But nobody has a definitive answer on architecture yet. The embedding interface is our bet — not because it's obviously right, but because it asks the right question: what should the interface between understanding and action look like?

We're building it. We'll report back when we have results.

---

*Kynetic Intelligence is building robot learning systems. One brain. Any robot.*
