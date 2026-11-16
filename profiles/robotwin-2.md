---
title: RoboTwin 2.0
area: robot-manipulation-benchmark
official_repo: https://github.com/RoboTwin-Platform/RoboTwin
---

# RoboTwin 2.0

## Snapshot

- **Primary purpose:** scalable data generation and robust bimanual manipulation evaluation.
- **Setting:** SAPIEN-based dual-arm simulation with multiple supported robot embodiments.
- **Task organization:** 50 bimanual tasks built around a diverse object collection.
- **Key variation:** clean and domain-randomized evaluation settings.

## Why It Matters

RoboTwin 2.0 connects three problems that are often treated separately: authoring manipulation tasks, generating expert demonstrations at scale, and evaluating learned policies under environmental variation. Its focus on dual-arm coordination and diverse objects makes it complementary to single-arm tabletop suites.

## Data and Evaluation

The framework includes programmable task experts, automated task-code generation tools, the RoboTwin Object Dataset, and policy evaluation. The official project describes 50 tasks, 731 objects across 147 categories, and support for five robot embodiments. Domain randomization varies factors such as objects, clutter, lighting, backgrounds, table height, and language instructions.

## Reading Results

- Report the exact task set and robot embodiment.
- Keep clean and randomized results separate.
- State whether training uses RoboTwin-generated demonstrations and how much data is used.
- Record scene seeds, episode count, step limits, language variants, and enabled randomizations.
- RoboTwin 2.0 and RoboDojo can share XPolicyLab integration, but they use different tasks and evaluation designs.

## Primary Sources

- [Official repository](https://github.com/RoboTwin-Platform/RoboTwin)
- [Project page](https://robotwin-platform.github.io/)
- [Documentation](https://robotwin-platform.github.io/doc/)
- [Paper](https://arxiv.org/abs/2506.18088)
- [Leaderboard](https://robotwin-platform.github.io/leaderboard/)
