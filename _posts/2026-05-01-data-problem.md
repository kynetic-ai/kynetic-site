---
layout: post
title: "The Data Problem"
date: 2026-05-01 22:30:00 -0500
categories: research
published: false
---

Everyone in robot learning agrees on the diagnosis: we need more data. The disagreement is about what kind of data, how to get it, and whether scaling alone will work.

The field has watched language models eat the internet and come out the other side capable of reasoning about things they've never seen. It's tempting to imagine the same story for robotics. Collect every trajectory from every robot in every lab. Train one big model. Ship.

I think this misses something fundamental about what makes robot data different from text.

## Robot Data Is Physically Expensive

Training GPT-5 costs money — a lot of it — but the training data is already sitting on servers. Every web page, every book, every GitHub repo already exists. You pay to process it, not to create it.

Robot data doesn't exist until someone runs a robot. Every trajectory costs: hardware time, operator attention, safety monitoring, the electricity to move motors against gravity. A single hour of real-world manipulation data might represent hundreds of dollars in direct costs and days of calendar time — the robot needs to be set up, the task needs to be staged, and someone needs to be there in case things go wrong.

This is not a temporary problem that better hardware will solve. Running a robot in the physical world will always cost more than reading a file from disk. The cost floor for physical data is set by physics, not engineering.

## Robot Data Is Siloed by Embodiment

This is the less obvious problem, and the one that matters more.

Language data is naturally unified. A paragraph about cooking is useful for training a model to write poetry, because the underlying structures — syntax, semantics, reasoning patterns — transfer. The medium is the same. The tokens are the same.

Robot data is not like this. A trajectory from a 7-DOF Franka arm is a sequence of joint positions, velocities, and torques in a specific kinematic structure. A trajectory from a Unitree H1 humanoid is a completely different tensor shape with different physical meaning. A trajectory from a wheeled base doesn't even have the same degrees of freedom.

If you train a model on Franka manipulation data, it learns something about reaching, grasping, and contact. But the learning is tangled up with the specific joint configuration of a Franka arm. Give it H1 data and it has to learn a completely different mapping from intent to motion — from scratch, because the tensor shapes don't even align.

This is the embodiment gap. Every robot speaks a different physical language. And unlike human languages, there's no shared substrate — no common alphabet of joint angles that works across a humanoid, a manipulator, and a mobile base.

## Simulation Helps, But It's Not Free

Simulation is the obvious answer: generate infinite data in silico. Isaac Sim, MuJoCo, SAPIEN — these are real tools that produce real results.

But simulation introduces its own problems.

**Domain randomization is expensive to tune.** You need to randomize lighting, textures, friction coefficients, actuator dynamics, sensor noise — and the space of possible randomizations is combinatorially large. Randomize too little and your policy doesn't transfer. Randomize too much and it never converges.

**Contact-rich tasks are still hard to simulate accurately.** Grasping an object, inserting a peg, opening a drawer — these involve discontinuous dynamics that simulators approximate with varying fidelity. A policy that works beautifully in simulation can fail on the first real contact because the friction model was 10% off.

**The sim-to-real gap for full-body control is large.** Humanoid locomotion in simulation is a solved problem. Humanoid locomotion on real hardware is not. The difference is unmodeled dynamics: cable drag, joint stiction, actuator backlash, ground compliance. These aren't bugs in the simulator — they're features of the physical world that no current simulator captures well.

## What Makes Cross-Embodiment Data Different

We're trying to solve a harder version of this problem. We don't just need data from one robot — we need data from multiple embodiments that can train a shared representation.

This means the data must go through a bottleneck that strips away embodiment-specific detail while preserving movement structure. A reaching motion on a Franka arm and a reaching motion on a H1 humanoid should map to nearby points in some shared space — not because they look similar (they don't), but because they mean the same thing: "move the end effector to the target."

Learning this mapping is the core technical challenge. It requires training across diverse embodiments simultaneously — sequential training causes the embedding space to drift. It requires careful balancing: if the bottleneck is too narrow, you lose information needed for control. If it's too wide, embodiment-specific details leak through and the representation doesn't transfer.

## Where This Leaves Us

I'm not saying the scaling approach is wrong. If someone collects 50,000 hours of manipulation data across 20 embodiments and trains a big enough model, they might get something useful. The question is whether that's the most efficient path — or even a feasible one.

The alternative is to be smarter about the architecture: build a system where the data from each embodiment teaches the shared representation something useful, rather than just teaching it about that specific robot's joint limits. That's what the embedding interface is for. It's not a shortcut around the data problem — it's an answer to the question of what form the data should take.

We need more robot data. But we also need better ways to use the data we have. The two problems are connected. You can't solve one without the other.

---

*Kynetic Intelligence is building robot learning systems. One brain. Any robot.*
