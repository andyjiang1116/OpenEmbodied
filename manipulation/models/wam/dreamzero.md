# DreamZero

[简体中文](dreamzero_ZH.md) · [World Action Models](README.md)

> Video-based world-action policy · [Paper](https://arxiv.org/abs/2602.15922) · [Project page](https://dreamzero0.github.io/) · [Official repository](https://github.com/dreamzero0/dreamzero)

<p align="center"><img src="https://dreamzero0.github.io/images/project_overview.png" alt="DreamZero video-action model and closed-loop execution overview" width="820" /></p>

<p align="center"><em>DreamZero method overview. Image: <a href="https://dreamzero0.github.io/">official project page</a>.</em></p>

## Technical Summary

DreamZero studies whether a pretrained video generative model can supply the physical-motion knowledge needed for robot control. It builds a World Action Model on a video diffusion backbone and jointly predicts future visual states and corresponding robot actions. The robot policy therefore learns from how the scene evolves, while retaining an executable action output. The paper focuses on generalization to new tasks, objects, environments, and robot embodiments.

## Inputs and Joint Video–Action Modeling

At each decision, DreamZero conditions on a language instruction, current proprioception, and current and previous visual observations. It predicts a horizon of future video and matching actions. State and action encoders and decoders adapt the pretrained video backbone to robot data; multiple camera views are combined into the visual input. A single end-to-end model jointly learns the video and action predictions rather than placing a separate inverse-dynamics model after a video generator.

Video is modeled autoregressively in chunks. During training, the model denoises video and action latents together using a flow-matching objective. At execution, it generates a short future segment, executes an action chunk, and replaces predicted observations with actual camera observations before the next generation. This correction limits the accumulation of video-prediction error. Caching, asynchronous execution, and lower-level model optimizations reduce the cost of repeatedly running a large video model.

## Data and Transfer Settings

The paper evaluates pretrained models on AgiBot and DROID data. Its AgiBot protocol distinguishes ten motions represented in training from ten motions absent from training, using unseen objects and environments for both groups. The DROID protocol evaluates 20 seen and 20 unseen tasks. Other experiments examine task-specific post-training and adaptation to a new YAM robot from a short period of play data. Human and other-robot videos are studied as video-only adaptation material; this is distinct from supplying labeled action trajectories.

## Reported Results and Boundaries

The authors report more than a twofold gain in task progress over their strongest compared pretrained VLA on specified real-robot generalization settings. They also report 7 Hz closed-loop control for a 14B video-action model after model and system optimizations. These are results under the paper's task selection, hardware, and rollout protocol; task progress is not identical to binary task success. The term “zero-shot” applies to the stated evaluation tasks and embodiments, not to training without robot data.

The official repository provides code for pretraining, fine-tuning, inference, and available simulation and real-robot evaluations. Reproduction requires the released model artifacts, compatible camera and proprioception inputs, action-space definitions, and substantial video-model compute. Evaluation should preserve the paper's distinctions between seen and unseen motions, new objects and environments, and adaptation with or without action labels.

## A Closed-Loop Decision Cycle

At a control step, DreamZero receives recent camera observations, the current robot state, and a language goal. It predicts a short future visual sequence together with the action sequence intended to produce it. The robot executes an action chunk, then the next model call uses real camera observations rather than treating the previously generated frames as ground truth. This replacement is what makes the method closed-loop: a mistaken visual prediction can be corrected after new evidence arrives, although errors within an executed chunk still matter.

The video backbone supplies a prior over scene evolution; action-labeled robot data connects that prior to the control space of a particular embodiment. Video-only material and robot demonstrations therefore play different roles. A generated future can illustrate what the model expects to happen, but task progress or success must be measured from actual rollouts. The reported 7 Hz execution is tied to the paper's optimized hardware and software path, not an inherent rate of every checkpoint.

## Where the Method Applies

DreamZero is relevant to language-conditioned manipulation where future scene evolution carries useful information, especially transfer tests over tasks, objects, environments, or embodiments. Its released workflow requires the matching visual inputs, proprioception, action convention, model weights, and substantial accelerator capacity. For a new platform, the evaluation must distinguish zero-shot task transfer from adaptation using new robot data; both appear in the paper but answer different questions.

## References

- [Paper: World Action Models are Zero-shot Policies](https://arxiv.org/abs/2602.15922)
- [Project page](https://dreamzero0.github.io/)
- [Official repository](https://github.com/dreamzero0/dreamzero)
