# LIBERO

[简体中文](libero_ZH.md)

> **Category:** Robot Manipulation Benchmark · [Repository](https://github.com/Lifelong-Robot-Learning/LIBERO) · [Project Page](https://libero-project.github.io/) · [Paper](https://arxiv.org/abs/2306.03310)

<p align="center">
  <img src="../../docs/assets/benchmarks/libero-overview.jpg" alt="LIBERO benchmark overview" width="820" />
</p>

<p align="center"><em>LIBERO studies knowledge transfer across language-conditioned manipulation tasks. Image source: <a href="https://libero-project.github.io/">official project page</a>.</em></p>

## Technical Summary

- **Primary purpose:** knowledge transfer in lifelong and multitask robot learning.
- **Setting:** language-conditioned tabletop manipulation in robosuite/MuJoCo.
- **Task organization:** spatial, object, goal, 10-task, and 90-task suites.
- **Typical output:** task success; lifelong-learning studies additionally measure transfer and forgetting.

## Evaluation Objective

LIBERO separates several sources of task variation so researchers can ask what knowledge moves between tasks. Spatial tasks change target relations, object tasks emphasize object identity, goal tasks vary the requested behavior, and larger suites test learning across broader task collections.

The benchmark is now also commonly used to evaluate VLA fine-tuning. That use is valid, but it answers a narrower question than the original lifelong-learning design unless tasks are learned sequentially and knowledge transfer is explicitly measured.

## Experimental Design

LIBERO provides procedurally defined manipulation tasks, language descriptions, demonstration datasets, and standardized suites. Policies usually receive visual observations, language, and optionally robot state, then produce continuous control actions. Exact camera inputs, history, control representation, rollout length, and demonstrations per task vary across later model papers and must be stated with results.

## Task Suites

- **LIBERO-Spatial** varies spatial relationships while keeping object and goal semantics comparatively controlled.
- **LIBERO-Object** emphasizes transfer across manipulated objects.
- **LIBERO-Goal** varies the target behavior or goal language.
- **LIBERO-10** contains downstream tasks for lifelong-learning evaluation.
- **LIBERO-90** contains tasks used for policy pretraining in the original LIBERO-100 design.

The suite names are part of the experimental definition. An average across four commonly used suites is useful for VLA evaluation, but it should not be confused with the sequential learning protocols used in the original benchmark.

## Evaluation and Transfer Protocols

### How an Evaluation Is Constructed

A task specifies an initial scene, a language instruction, and a success condition. A policy receives observations, predicts actions, and is rolled out until it succeeds or reaches the episode limit. The resulting success rate is the fraction of trials that satisfy the task condition. The number of initial states and rollouts matters because a task can be easy from one placement and difficult from another. Image views, proprioception, action frequency, and training demonstrations also define the experiment, even when the task name is unchanged.

In the original lifelong-learning setting, tasks arrive as a sequence. A learner updates on later tasks without freely revisiting all earlier demonstrations, and is evaluated again on earlier tasks. This makes forgetting measurable. By contrast, a VLA model fine-tuned jointly on a suite is a multitask policy; its final average success does not measure lifelong transfer. LIBERO-90 and LIBERO-10 have distinct roles in the original LIBERO-100 protocol, so their names should not be treated as interchangeable difficulty levels.

### Interpreting Transfer

Forward transfer concerns whether experience on earlier tasks helps learning a later one. Backward transfer concerns how later learning changes performance on earlier tasks; a negative change is forgetting. These quantities require a learning order and repeated evaluation, whereas ordinary task success needs only a fixed policy and rollout set. To compare two studies, first identify the suite, task order, training regime, observation modalities, and whether any external pretraining data were used.

## Metrics and Research Use

Independent rollouts typically report binary task success. Lifelong-learning experiments additionally care about forward transfer, backward transfer, and forgetting after learning a sequence of tasks. The benchmark is therefore useful for both policy adaptation and continual learning, provided the reported metric matches the claim.

## Reading Results

- Name the exact suite rather than reporting “LIBERO” alone.
- Separate multitask training from sequential lifelong learning.
- Do not infer resistance to forgetting from final average success alone.
- Check whether extra data, observation history, multiple camera views, or benchmark-specific fine-tuning were used.

## Research Use

Use LIBERO for controlled comparisons of language-conditioned tabletop policies, data-efficient adaptation, or sequential knowledge transfer. It is less suitable for claims about bimanual coordination, real-world deployment, or broad sim-to-real robustness.

## References

- [Official repository](https://github.com/Lifelong-Robot-Learning/LIBERO)
- [Project page](https://libero-project.github.io/)
- [Paper](https://arxiv.org/abs/2306.03310)
