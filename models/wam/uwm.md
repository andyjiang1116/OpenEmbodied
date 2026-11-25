# Unified World Models

[简体中文](uwm_ZH.md) · [World Action Models](README.md)

> Coupled video and action diffusion · [Paper](https://arxiv.org/abs/2504.02792) · [Project page](https://weirdlabuw.github.io/uwm/) · [Official repository](https://github.com/WEIRDLabUW/unified-world-model)

<p align="center"><img src="https://arxiv.org/html/2504.02792v3/teaser.png" alt="Unified World Models: video and action diffusion with modality-specific timesteps" width="820" /></p>

<p align="center"><em>Video and action diffusion in one model. Figure: <a href="https://arxiv.org/abs/2504.02792">original paper</a>.</em></p>

## Technical Summary

Unified World Models (UWM) addresses a limitation of imitation learning: action-labeled robot demonstrations are expensive, while videos contain useful information about how objects move and interact without recording the actions that produced them. UWM trains one diffusion transformer over future visual observations and robot actions. Independent diffusion timesteps for the two modalities let the same trained model act as a policy, predict future observations, infer actions between observations, or generate video. Its central contribution is the coupling of action learning and world modeling within one training objective.

## Inputs, Outputs, and Model Design

The model receives the current visual observation, a noisy candidate action chunk, a noisy future-observation sequence, and a separate noise level for each predicted modality. A diffusion transformer predicts the noise in the action and video tokens. Camera frames and action chunks have defined history and prediction horizons; the robot action dimensions and normalization must match the dataset and embodiment.

During training, action and video noise levels are sampled independently. The shared network therefore sees examples in which both modalities are uncertain, one is known and the other is uncertain, or one modality is absent. Register tokens and a shared transformer allow information to pass between visual and action features. A video without action labels can contribute to the visual objective without being presented as a complete robot trajectory.

## Four Inference Uses

| Use | Given | Generated |
| --- | --- | --- |
| Policy | Current observation | Action chunk; future observation is marginalized by fixing it at maximum noise |
| Video prediction | Current observation | Future observations; action is marginalized |
| Forward dynamics | Current observation and an action | Resulting future observations |
| Inverse dynamics | Current and target observations | Action connecting the two |

The diffusion timestep settings select these conditional distributions. This flexibility does not mean that every generated future frame is suitable for planning: the paper notes that visual reconstructions can contain artifacts.

## Training Data and Evaluation

For the real-robot study, the authors sample 2,000 action-labeled DROID trajectories for pretraining and a separate 2,000 trajectories whose action labels are removed for video co-training. They evaluate five manipulation tasks on a DROID-style robot, including bowl stacking and cabinet placement, under in-distribution and changed conditions. In simulation, LIBERO-90 supplies multitask training tasks and five selected LIBERO-10 environments support downstream evaluation. These settings test whether joint dynamics supervision and action-free video improve a policy after adaptation; they do not establish a universal ranking against other model families.

The paper also evaluates forward and inverse dynamics and ablates the training objectives. Its stated limits include incomplete transfer from large-scale human video and artifacts in predicted observations. When comparing results, the robot platform, number and type of pretraining trajectories, fine-tuning data, image views, action horizon, and evaluation split must be aligned.

## Public Implementation

The official PyTorch repository contains configurations and scripts for Robomimic, LIBERO, and DROID. It converts datasets into compressed Zarr buffers and provides separate pretraining, video co-training, fine-tuning, and evaluation workflows. The repository links released DROID checkpoints. Reusing a checkpoint on another robot requires compatible observations, action coordinates, normalization, and task data; the published workflows do not provide a platform-independent controller.

## References

- [Paper](https://arxiv.org/abs/2504.02792)
- [Project page](https://weirdlabuw.github.io/uwm/)
- [Official repository](https://github.com/WEIRDLabUW/unified-world-model)
