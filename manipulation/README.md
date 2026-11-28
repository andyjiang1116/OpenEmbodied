# Embodied Manipulation

[简体中文](README_ZH.md) · [Home](../README.md)

Robot manipulation methods differ in what they predict and where their outputs enter the control loop. This page organizes four method families—VLA policies, World-Action Models (WAMs), agent-based systems, and grasping models—and links their technical profiles and evaluation benchmarks.

## Contents

- [Model profiles](models/README.md): VLA, WAM, and grasping models.
- [Agent-based systems](agents/README.md): tool use, policy supervision, and recovery.
- [Evaluation benchmarks](benchmarks/README.md): tasks, metrics, and protocols.
- [VLA technical analysis](analysis/vla/README.md): architecture, action representations, and evaluation conditions.

## Method Families at a Glance

| Family | Input and immediate output | Main role |
| --- | --- | --- |
| [VLA](models/vla/README.md) | Images, instruction, and often robot state → action or action chunk | Learned language-conditioned controller |
| [WAM](models/wam/README.md) | Observations and often language → actions with world-dynamics modeling | Policy trained with visual dynamics or future prediction |
| [Agent-based system](agents/README.md) | Observations, task, history, and tools → tool call, motion target, or intervention | Decision and recovery around a controller |
| [Grasping model](models/grasping/README.md) | Object or scene geometry → candidate gripper or hand grasp | Contact proposal for a manipulation pipeline |

The categories describe components rather than mutually exclusive robots. An agent can review a VLA trajectory; a grasp model can propose a target executed by a learned policy.

## Vision-Language-Action Policies

A VLA policy turns visual observations and a language goal into robot actions. The camera and state fields, action representation, and normalization must match the target robot. The four projects below illustrate different ways to implement that mapping.

| Method | Action generation | Distinguishing interface |
| --- | --- | --- |
| [OpenVLA / OpenVLA-OFT](models/vla/openvla.md) | Original model: discrete action tokens; OFT: continuous actions and chunks | Open X-Embodiment lineage and distinct fine-tuning recipes |
| [SmolVLA](models/vla/smolvla.md) | Flow-matching continuous action chunks | Compact model integrated with LeRobot data and robot tools |
| [openpi: π0 / π0-FAST / π0.5](models/vla/openpi.md) | Flow matching for π0 and π0.5; autoregressive FAST tokens for π0-FAST | Multiple checkpoints and robot-specific data transforms in one repository |
| [GR00T N1.7](models/vla/gr00t-n1.7.md) | Flow-matching action transformer | Embodiment configurations and documented serving paths |

**Where it fits.** VLA policies are relevant when demonstrations specify the action behavior and the task is conditioned on visual and language input. A base checkpoint normally still needs adaptation to the target embodiment.

**What to compare.** Record the exact checkpoint, camera views, robot-state fields, action units, normalization, fine-tuning data, chunk length, and control rate. The [VLA comparison](analysis/vla/README.md) expands the architecture and resource differences; its [evaluation notes](analysis/vla/benchmark-notes.md) cover protocol alignment.

## World-Action Models

WAMs connect action learning to scene evolution. The important distinction is **when** world modeling is used: as a training objective, as generated future observations during inference, or both. Video quality and physical task success are separate outcomes.

| Method | World-action coupling | Action-time behavior |
| --- | --- | --- |
| [Unified World Models](models/wam/uwm.md) | Joint video-action diffusion with separate noise levels | The same weights support policy and dynamics queries under different conditioning |
| [DreamZero](models/wam/dreamzero.md) | Joint prediction of future video and actions | Executes a short chunk, then replaces predictions with new observations |
| [Fast-WAM](models/wam/fast-wam.md) | Video prediction during training | Direct action generation without explicit future-video generation |
| [OpenWAM](models/wam/openwam.md) | Modular study of backbones, information flow, and pretraining | OpenWAM-α provides a released pretrained policy |

**Where it fits.** WAMs are relevant when scene dynamics, video prediction, or action-free video are part of the research problem. They can be studied as controllers, world predictors, or both, depending on the released method.

**What to compare.** Identify the video backbone, training data, action representation, prediction horizon, denoising steps, whether video is generated while acting, and measured inference latency. A faster policy may differ because it omits a video-generation stage rather than because its action model is intrinsically smaller.

## Agent-Based Manipulation

Agent-based systems add a decision layer around robot tools or learned policies. The key design choice is **control authority**: who proposes motion, who validates it, and when an agent takes or returns control.

| System | Agent's decision | Control boundary |
| --- | --- | --- |
| [GPT-6 Astra as an Embodied Policy](agents/gpt-as-policy.md) | Direct end-effector targets, or acceptance/correction of a π0.5 proposal | Host validates targets and executes bounded segments |
| [π0.5 + Astra with Selective Intervention](agents/pi05-call-astra.md) | Recovery after a local CALL detector triggers | Frozen π0.5 remains the ordinary controller |
| [GPT-Policy](agents/gpt-policy.md) | Structured robot-tool requests informed by demonstrations and feedback | Tool adapters convert requests into executable motion |

**Where it fits.** These systems address task decomposition, changing instructions, and recovery when a fixed low-level policy is insufficient. They still depend on controller limits, coordinate conversion, and robot feedback.

**What to compare.** Report task success together with agent-call frequency, actual executed interventions, decision latency, tool validation, and how the simulator or robot advances while the agent reasons. A consultation that returns control without acting is different from an executed correction.

## Grasping Models

Grasping models estimate where and how an end effector can contact an object. A candidate grasp is not a complete pick-and-place plan: calibration, reachability, approach motion, finger closure, and outcome verification remain separate steps.

| Method | End effector and output | Main distinction |
| --- | --- | --- |
| [AnyGrasp](models/grasping/anygrasp.md) | Parallel gripper; six-degree-of-freedom grasp poses | Point-cloud detection and temporal tracking |
| [UniDexGrasp](models/grasping/unidexgrasp.md) | Dexterous hand; proposals plus execution policy | Separates target generation from goal-conditioned control |
| [DexGraspNet 2.0](models/grasping/dexgraspnet-2.md) | Dexterous hand; scene-conditioned poses | Accounts for clutter around the target |
| [DexGrasp Anything](models/grasping/dexgrasp-anything.md) | Dexterous hand; generative poses | Applies physical constraints during diffusion sampling |

**Where it fits.** Parallel-gripper detection supports grasp selection in picking systems. Dexterous methods address articulated-hand contact and grasp generation, sometimes with a separate execution policy.

**What to compare.** Match the hand model and scene conditions. Report pose validity, collision freedom, simulated lift success, and real-robot task completion separately; these metrics test different stages.

## Comparing Complete Systems

To compare two approaches, trace one observation through the complete loop:

1. **Observe:** identify cameras, state fields, task instructions, and history.
2. **Predict:** name the model's immediate output—action, video, grasp, tool call, or intervention.
3. **Execute:** record decoding, normalization, planning, controller constraints, and action timing.
4. **Re-observe:** state when fresh observations replace predictions and whether the world advances during inference.
5. **Evaluate:** align robot, training data, checkpoint, task distribution, seeds, success rule, and metric aggregation.

The [benchmark index](benchmarks/README.md) explains which capabilities each evaluation suite measures and how its protocol affects interpretation.
