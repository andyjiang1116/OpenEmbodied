# World Action Models

[简体中文](README_ZH.md) · [Models](../README.md) · [Manipulation paradigms](../../analysis/manipulation-paradigms/README.md)

World Action Models (WAMs) connect robot action prediction with modeling how the observed world changes. The term covers different training objectives and inference procedures; future-video generation may occur during training, deployment, or both.

| Method | World-action coupling | Inference behavior |
| --- | --- | --- |
| [Unified World Models](uwm.md) | Joint video and action diffusion, with separately controlled diffusion timesteps | Supports policy and world-prediction uses within one model |
| [DreamZero](dreamzero.md) | Pretrained video diffusion backbone jointly models future video and actions | Generates world and action trajectories for closed-loop control |
| [Fast-WAM](fast-wam.md) | Video prediction co-training shapes latent world representations | Predicts actions without explicit future-video generation |
| [OpenWAM](openwam.md) | Modular study of video backbones, world-action coupling, and embodied pretraining | OpenWAM-α combines world and action modeling for policy inference |

These methods should be compared by the role of video data, action representation, training data, observation interface, inference latency, and robot embodiment. See the [cross-paradigm analysis](../../analysis/manipulation-paradigms/README.md).
