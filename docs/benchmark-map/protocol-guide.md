# Protocol Guide

[简体中文](protocol-guide_ZH.md)

[Overview](README.md) · [Benchmark matrix](benchmark-matrix.md) · [Sources](sources.md)

## Before Comparing Two Results

Check the following fields in the paper, repository, or evaluation configuration:

1. **Benchmark release and task suite** — confirm the same tasks, split, assets, and simulator version.
2. **Training data** — distinguish official demonstrations, extra robot data, synthetic data, and benchmark-specific fine-tuning.
3. **Observation interface** — list camera views, resolution, proprioception, language, history, and privileged state.
4. **Action interface** — identify joint or Cartesian control, absolute or delta actions, control frequency, action chunking, and post-processing.
5. **Initial-state distribution** — note scene seeds, object placements, clean/randomized settings, and reset rules.
6. **Rollout protocol** — record time limit, termination condition, number of episodes, seeds, and retry policy.
7. **Checkpoint selection** — separate the last checkpoint from validation-selected or task-selected checkpoints.
8. **Metric aggregation** — determine whether results average tasks, episodes, suites, chain lengths, capability dimensions, or robot stations.
9. **Inference timing** — state whether the environment pauses during policy inference and record measured latency when task dynamics continue.

## Benchmark-Specific Reading

### LIBERO

- Name the suite: `LIBERO-Spatial`, `LIBERO-Object`, `LIBERO-Goal`, `LIBERO-10`, or `LIBERO-90`.
- Distinguish multitask training from sequential lifelong learning.
- For lifelong learning claims, report the task order and the transfer/forgetting measure—not only final success.
- Record image views, state inputs, demonstrations per task, and rollout horizon.

### CALVIN

- Identify the dataset split and whether evaluation uses language annotations.
- Report the five values for completing at least 1 through 5 consecutive instructions, plus the average sequence length.
- State whether the policy observes history and whether it resets internal state between subtasks.
- Do not replace the official chained evaluation with independent atomic-task success while retaining the same benchmark label.

### SimplerEnv

- Name the robot and task family, such as Google Robot or WidowX setups.
- State whether the run uses visual matching or environment-variant aggregation.
- Match policy checkpoints and observation/action transforms to the real-world evaluation being approximated.
- Report correlation or ranking agreement with the paired real results when making a sim-to-real fidelity claim.

### RoboTwin 2.0

- Identify the task list and robot embodiment.
- Separate clean and randomized evaluations and describe enabled randomizations.
- Record the number of episodes per task, scene seeds, language variants, and evaluation step limits.
- Distinguish results using RoboTwin-generated training data from zero-shot or externally trained policies.

### RoboDojo

- Report the five simulation dimensions separately: generalization, memory, precision, long-horizon, and open.
- Distinguish simulation, remote real-world evaluation, and any locally reproduced setup.
- Record benchmark layouts, seeds, XPolicyLab policy adapter, action interface, and submitted checkpoint.
- Use the official scoring and verification protocol when comparing against the public leaderboard.

### RoboDyna

- Report synchronous and asynchronous results separately on the same task conditions and seeds.
- Record measured policy latency, inference hardware, and whether communication or preprocessing time is included.
- Identify conceptual versus household tasks and the `base`, `var1`, `var2`, or held-out `var1+2` condition.
- Report success rate together with progress score when partial completion is relevant.
- Do not compare a frozen-world result with a real-time result as if they used the same protocol.

## Minimum Result Record

A reusable result entry should contain:

```text
Model and checkpoint:
Training data and adaptation:
Benchmark version and tasks:
Robot and simulator:
Observations and actions:
Episodes, seeds, and horizon:
Metric and aggregation:
Hardware and policy frequency:
Inference latency and timing protocol:
Source:
```

This information does not make different benchmarks numerically comparable. It makes each reported result understandable and repeatable.
