# Robot Manipulation Paradigms

[简体中文](README_ZH.md) · [Research analysis](../README.md) · [Home](../../README.md)

Robot manipulation systems differ in what they predict, where control decisions are made, and how frequently observations enter the loop. The categories below describe system design rather than a ranking of capability. A single system can combine several categories.

## Learned Vision-Language-Action Policies

[VLA models](../../models/vla/README.md) map visual observations, language instructions, and often robot state to action tokens or continuous action chunks. OpenVLA, SmolVLA, openpi, and GR00T differ in backbone, action representation, training data, and embodiment interface. Their action predictions can serve as the low-level component of a larger agent system. See the [VLA comparison](../vla/README.md).

## World Action Models

[World Action Models](../../models/wam/README.md) learn actions together with how observations evolve. [Unified World Models](../../models/wam/uwm.md) couples video and action diffusion; [DreamZero](../../models/wam/dreamzero.md) uses a pretrained video backbone for joint world-action prediction; [Fast-WAM](../../models/wam/fast-wam.md) retains video co-training but skips explicit future-video generation during inference. [OpenWAM](../../models/wam/openwam.md) provides a modular framework for studying world-action pretraining and releases the OpenWAM-α policy. Thus, “WAM” does not imply one fixed test-time imagination procedure.

## Agent-Based Control

[Agent-based manipulation systems](../../systems/agents/README.md) use a multimodal reasoning model within an observation–decision–execution–feedback loop. The agent may generate bounded robot commands directly, review a learned policy's candidate trajectory, or take control only when recovery is needed. [GPT-6 Astra as an Embodied Policy](../../systems/agents/gpt-as-policy.md), [π0.5 + Astra with Selective Intervention](../../systems/agents/pi05-call-astra.md), and [GPT-Policy](../../systems/agents/gpt-policy.md) illustrate these distinct control interfaces. Tool validation and low-level control are part of the system, so results cannot be attributed to the language model alone.

## Grasping Components

[Grasping models](../../models/grasping/README.md) estimate candidate grasps or generate dexterous-hand configurations. They may supply perception or action proposals to VLA, WAM, or agent-based systems. A predicted grasp pose still requires coordinate transforms, feasibility checks, motion planning, and execution.

## Comparison Dimensions

| Dimension | Questions to record |
| --- | --- |
| Prediction target | Robot actions, future observations, grasp poses, or tool calls? |
| Control interface | Joint actions, end-effector targets, skill calls, or candidate-policy review? |
| Training signal | Robot demonstrations, video prediction, action-free video, or in-context examples? |
| Execution loop | Action-chunk horizon, observation frequency, inference latency, and physical time progression? |
| System boundary | Which planner, controller, inverse kinematics, safety constraints, and recovery logic are external to the model? |
| Evaluation | Task suite, embodiment, seeds, success criteria, runtime, and matched baselines? |

Benchmark scores are comparable only within aligned tasks and protocols. The [manipulation benchmark comparison](../manipulation-benchmarks/README.md) describes those protocol differences.
