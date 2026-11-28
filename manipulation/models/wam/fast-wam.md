# Fast-WAM

[简体中文](fast-wam_ZH.md) · [World Action Models](README.md)

> Video co-training without test-time future-video generation · [Paper](https://arxiv.org/abs/2603.16666) · [Project page](https://yuantianyuan01.github.io/FastWAM/) · [Official code](https://github.com/yuantianyuan01/FastWAM)

<p align="center"><img src="https://yuantianyuan01.github.io/FastWAM/static/images/model_arch.png" alt="Fast-WAM shared-attention video backbone and action expert architecture" width="820" /></p>

<p align="center"><em>Video backbone, action expert, and training/inference paths. Image: <a href="https://yuantianyuan01.github.io/FastWAM/">official project page</a>.</em></p>

## Technical Summary

Fast-WAM isolates two ideas often combined in World Action Models: learning from future-video prediction during training and explicitly generating future frames before choosing an action at test time. The method retains the video-prediction objective but omits future-video generation while acting. This makes its runtime interface resemble a direct action policy while the learned representation still receives world-model supervision.

## Inputs and Architecture

The model conditions on the current visual observation and task language, encodes images through a video VAE, and generates a robot action chunk. Its backbone is a pretrained Wan2.2-5B video Diffusion Transformer with a separate action expert. A shared-attention Mixture-of-Transformer design lets action tokens use visual context while preserving modality-specific processing.

During training, noisy future-video tokens and action tokens are optimized together. The attention mask prevents action tokens from reading future-video tokens, so action prediction cannot rely on information unavailable during deployment. At inference, the future-video tokens are removed. The video backbone processes the current-frame latent tokens once, and the action expert denoises the action chunk from this latent representation. This is the central difference from “imagine, then execute” WAMs, which synthesize a future before action generation.

## Controlled Variants

The paper compares the direct-inference model with joint video–action denoising, an imagine-then-act variant, and a variant trained without video co-training. The comparison is designed to separate the effect of the training objective from the cost and potential benefit of future generation. An additional released Optional IDM checkpoint can run in `idm` mode, which predicts future video before actions, or `first_frame` mode, which predicts actions from the current frame without retraining.

## Evaluation and Reported Results

The paper evaluates LIBERO, RoboTwin 2.0, and real-robot towel folding. On RoboTwin 2.0, the reported average is 91.8% for Fast-WAM, 90.6% for the joint-generation variant, 91.3% for the imagine-then-act variant, and 83.8% without video co-training. These comparisons support the paper's conclusion that video supervision during training contributes more than explicit future generation in these settings. They do not imply the same ordering on every robot or task distribution.

The original project page reports 190 ms inference on one RTX 5090D V2 32 GB GPU and contrasts this with 810 ms for its imagine-then-act variant in the reported real-robot setting. The code repository also documents later inference optimizations on different GPUs. Hardware, compilation, text-embedding cache, and whether video decoding is included all affect measured latency; figures from these configurations should not be mixed.

## Public Implementation and Comparison Conditions

The official repository contains training and evaluation workflows for LIBERO and RoboTwin, including LeRobot 2.1 and 3.0 dataset support. Released checkpoints include LIBERO and RoboTwin models plus the Optional IDM variant, each paired with dataset statistics. Reproducing a reported score requires the matching data configuration, checkpoint and normalization statistics, evaluation task set, action scheduler shift, and runtime settings. The published real-robot demonstration uses a specific platform and does not establish drop-in control on other embodiments.

## Why Video Training Need Not Imply Video Inference

Fast-WAM uses future-video prediction as a training signal. The action tokens are deliberately prevented from attending to future-video tokens, so the action branch learns from the present visual context rather than reading a target that will be absent at deployment. After training, the future-video branch can be omitted from the control path. The action expert then denoises an action chunk from current-frame features without first generating a future movie. This design separates the possible representation benefit of video supervision from the latency cost of explicit future generation.

The distinction is observable in the paper's controlled variants: one removes video co-training, another generates video jointly at inference, and an imagine-then-act variant uses generated futures before action prediction. Those variants test specific architectural choices under matched tasks. Their reported scores do not establish that future generation is always unnecessary; another task may need a different horizon or world-state representation.

## Using the Released Checkpoints

The codebase supplies task-specific checkpoints and matching normalization statistics. A deployment must pair the checkpoint with the corresponding observation layout, action mapping, denoising settings, and evaluation client. The Optional IDM checkpoint has its own `idm` and `first_frame` modes; its existence should not be taken to mean every released Fast-WAM checkpoint supports both paths. Fast-WAM is relevant when control latency makes explicit video generation expensive but video prediction remains a useful training objective.

## References

- [Paper](https://arxiv.org/abs/2603.16666)
- [Project page](https://yuantianyuan01.github.io/FastWAM/)
- [Official code](https://github.com/yuantianyuan01/FastWAM)
- [Released checkpoints](https://huggingface.co/yuanty/fastwam)
