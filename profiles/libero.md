---
title: LIBERO
area: robot-manipulation-benchmark
official_repo: https://github.com/Lifelong-Robot-Learning/LIBERO
---

# LIBERO

## Snapshot

- **Primary purpose:** knowledge transfer in lifelong and multitask robot learning.
- **Setting:** language-conditioned tabletop manipulation in robosuite/MuJoCo.
- **Task organization:** spatial, object, goal, 10-task, and 90-task suites.
- **Typical output:** task success; lifelong-learning studies additionally measure transfer and forgetting.

## Why It Matters

LIBERO separates several sources of task variation so researchers can ask what knowledge moves between tasks. Spatial tasks change target relations, object tasks emphasize object identity, goal tasks vary the requested behavior, and larger suites test learning across broader task collections.

The benchmark is now also commonly used to evaluate VLA fine-tuning. That use is valid, but it answers a narrower question than the original lifelong-learning design unless tasks are learned sequentially and knowledge transfer is explicitly measured.

## Experimental Design

LIBERO provides procedurally defined manipulation tasks, language descriptions, demonstration datasets, and standardized suites. Policies usually receive visual observations, language, and optionally robot state, then produce continuous control actions. Exact camera inputs, history, control representation, rollout length, and demonstrations per task vary across later model papers and must be stated with results.

## Reading Results

- Name the exact suite rather than reporting “LIBERO” alone.
- Separate multitask training from sequential lifelong learning.
- Do not infer resistance to forgetting from final average success alone.
- Check whether extra data, observation history, multiple camera views, or benchmark-specific fine-tuning were used.

## Primary Sources

- [Official repository](https://github.com/Lifelong-Robot-Learning/LIBERO)
- [Project page](https://libero-project.github.io/)
- [Paper](https://arxiv.org/abs/2306.03310)
