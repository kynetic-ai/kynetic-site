---
layout: post
title: "One Brain. Any Robot."
date: 2026-05-01 18:30:00 -0500
categories: vision
---

Four words. That's the whole ambition.

**One brain. Any robot.**

I picked this tagline because it says what we're doing and what we're not doing. We're not building a brain for humanoids. We're not building a brain for arms. We're building one architecture that works across embodiments — and we mean *across*. A Unitree H1 walking through a kitchen and a Franka arm manipulating objects and a wheeled base navigating a warehouse should all run on the same system.

This sounds like science fiction. A year ago, I would have told you it was. But something shifted in 2025-2026. The pieces are coming together.

## Why One Brain?

The alternative — one model per robot, one training run per task — is the path the field has been on for decades. It works. It ships. It's also a dead end if you care about generalization.

Every time you build a embodiment-specific system, you solve the problem for that robot. You don't solve it for the next one. The knowledge doesn't transfer. The data doesn't compound. You start over.

One brain means data from a manipulator teaches a humanoid something useful. It means a skill learned in simulation deploys on hardware without retraining the whole stack. It means your investment in training compounds across every embodiment you add.

This is the economic argument. The scientific argument is simpler: intelligence that only works in one body isn't intelligence. It's a control policy. If we're serious about building systems that understand the physical world, they need to understand it in a way that's independent of any particular set of joints and actuators.

## Why Any Robot?

Because the hard part of robotics isn't any specific robot. It's the interface between knowledge and understanding and action — between knowing what to do and knowing how to move.

If you solve that interface, the embodiment becomes a detail. You train a low-level controller per platform — something that knows how a specific set of motors responds to commands — and you connect it to a shared high-level system that knows what to do in the world. The high-level system gets better with every robot you add. The low-level controllers stay cheap and specific.

We've written about the architecture that makes this possible: a learned embedding space that sits between task-level intent and embodiment-level control. The embedding captures movement structure. The controllers decode it for their hardware. The VLA driving the whole thing gets smarter with every interaction.

One brain. Any robot. We mean it.

— Miguel
