# RoboDyna

[简体中文](robodyna_ZH.md)

> **Category:** Robot Manipulation Benchmark · [Repository](https://github.com/RoboDyna/robodyna) · [Project Page](https://robodyna.github.io/robodyna/) · [Paper](https://arxiv.org/abs/2611.26969) · [Data & Assets](https://huggingface.co/RoboDyna)

<p align="center">
  <img src="https://robodyna.github.io/robodyna/figures/fig1_teaser.png" alt="RoboDyna benchmark overview" width="860" />
</p>

<p align="center"><em>RoboDyna evaluates language-conditioned dual-arm manipulation in worlds that continue evolving while a policy thinks. Image source: <a href="https://robodyna.github.io/robodyna/">official project page</a>.</em></p>

## Technical Summary

- **Primary purpose:** evaluate physical understanding and closed-loop action in dynamic scenes.
- **Environment:** language-conditioned dual-arm manipulation in SAPIEN 3.
- **Task organization:** 20 conceptual tasks across five capability categories and 10 household tasks.
- **Data:** 3,500 expert demonstrations from task-specific controllers.
- **Distinctive protocol:** paired synchronous and asynchronous evaluation on identical seeds.

## Evaluation Objective

Most manipulation benchmarks present a scene, wait for policy inference, execute an action, and then advance the environment. That design removes computation time from the task. RoboDyna instead studies a world governed continuously by gravity, friction, collision, contact, and state changes. Under its asynchronous protocol, the scene continues evolving for the measured inference duration, so a late action can become a wrong action.

This makes RoboDyna useful for separating three questions that static benchmarks often combine: whether a policy understands physical dynamics, whether it chooses an effective action, and whether it produces that action quickly enough.

## Capability Categories

- **Trajectory Prediction:** anticipate where a moving object will be, including motion redirected by contact or collision.
- **Periodic Pattern:** identify recurring motion and act within short opportunity windows.
- **Dynamic Avoidance:** plan robot motion around independently moving objects and obstacles.
- **State Transition:** track changes not captured by pose alone, such as ripeness, doneness, or availability.
- **Static to Dynamic:** anticipate motion caused by the robot itself through pushing, striking, or releasing.

Each category contains four conceptual tasks with minimal scene clutter. The 10 household tasks place related capabilities in richer office and kitchen scenes with phenomena such as rising liquids, overflow, dispensing, and spreading spills.

## Difficulty Design

Every conceptual task has four conditions:

- `base`: the easy condition;
- `var1` and `var2`: medium conditions that introduce one task-specific variation each;
- `var1+2`: the hard composition of both variations, withheld from training.

This design distinguishes robustness to one known variation from compositional generalization to a combined condition.

## Synchronous and Asynchronous Evaluation

The paired protocols use the same tasks and seeds but treat inference time differently:

- **Synchronous:** the environment is effectively frozen while the policy computes its next action.
- **Asynchronous:** the environment continues evolving for the measured inference latency before the action is applied.

The official study reports that latency changes the outcome of 5–12% of episodes, even though the change in average success rate is smaller. This means an aggregate average can hide meaningful timing failures at the episode level.

## Metrics and Baselines

RoboDyna reports binary success and a progress score that credits task milestones while penalizing errors. The paper evaluates π0.5, X-VLA, and FastWAM across 5.4K episodes and includes human baselines on matched seeds. Results are separated by difficulty, household tasks, capability category, metric, and sync/async protocol.

The reported policy results should be read as findings under the released checkpoints and protocol, not as a permanent ranking of model families. Human performance is also split by teleoperation and scene-interactive control because low-level control cost changes the task.

## Reading Results

- Report synchronous and asynchronous results separately; an average alone hides latency sensitivity.
- Record measured inference latency and the hardware used to obtain it.
- Identify `base`, `var1`, `var2`, and held-out `var1+2` conditions.
- Separate conceptual and household tasks, as they differ in clutter and semantic complexity.
- Report both success rate and progress score when partial completion matters.
- Keep policy and human control modes distinct.

## Why Inference Time Changes the Task

For a static scene, a policy can often use the newest image even if the computation that produced its action is slow. In a dynamic scene, the observed position may already be obsolete by the time the action reaches the robot. RoboDyna makes this difference explicit by evaluating identical task conditions under a frozen-world protocol and under one that advances physics during inference. A changed outcome can therefore be related to timing, although the size of that effect also depends on controller frequency, action horizon, and how latency was measured.

The conceptual tasks isolate particular physical phenomena, while household tasks combine them with clutter and semantic context. `var1+2` tests whether two variations can be handled together when their combination was withheld from training. A progress score gives partial credit for intermediate milestones but must be interpreted alongside binary success and error penalties. For reproducible results, the evaluation record should include the policy checkpoint, task condition, seed, inference hardware, latency boundary, and whether an episode used synchronous or asynchronous time.

## Research Use

Use RoboDyna when the research claim concerns dynamic physical reasoning, time-critical action, latency-aware evaluation, or compositional generalization under physically grounded motion. It complements static manipulation suites; it does not replace benchmarks designed specifically for lifelong transfer, long-horizon instruction chains, or standardized real-robot evaluation.

## References

- [Official repository](https://github.com/RoboDyna/robodyna)
- [Project page and task gallery](https://robodyna.github.io/robodyna/)
- [Paper](https://arxiv.org/abs/2611.26969)
- [Data and assets](https://huggingface.co/RoboDyna)
