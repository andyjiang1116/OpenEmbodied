---
title: CALVIN
area: robot-manipulation-benchmark
official_repo: https://github.com/mees/calvin
---

# CALVIN

## Snapshot

- **Primary purpose:** language-conditioned, long-horizon manipulation.
- **Setting:** a Franka arm in a PyBullet tabletop environment.
- **Task organization:** 34 atomic tasks that can be composed into instruction sequences.
- **Representative metric:** average number of consecutive instructions completed in a five-instruction chain.

## Why It Matters

CALVIN evaluates more than isolated reach-and-grasp success. A policy must interpret a changing sequence of language goals, preserve relevant context, transition between subtasks, and avoid errors that prevent later goals. This exposes compounding error and temporal composition more clearly than independent one-step trials.

## Data and Evaluation

The dataset contains teleoperated play interactions paired with language annotations for task-relevant segments. The standard long-horizon evaluation samples sequences of five instructions. Reporting commonly includes success at completing at least one, two, three, four, and all five instructions, plus the average completed sequence length.

## Reading Results

- Confirm the dataset split and official task-chain evaluation.
- Check whether history, language relabeling, auxiliary data, or pretrained vision-language components are used.
- Atomic-task success and chained success are not interchangeable.
- A strong first-task score with a steep chain-length decline indicates a different failure mode from uniformly low success.

## Primary Sources

- [Official repository](https://github.com/mees/calvin)
- [Project page](http://calvin.cs.uni-freiburg.de/)
- [Paper](https://arxiv.org/abs/2112.03227)
