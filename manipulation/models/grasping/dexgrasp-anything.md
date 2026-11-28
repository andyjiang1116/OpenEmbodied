# DexGrasp Anything

[简体中文](dexgrasp-anything_ZH.md) · [Grasping models](README.md)

> Universal dexterous grasp generation with physics-aware diffusion · [Project](https://dexgraspanything.github.io/) · [Code](https://github.com/4DVLab/DexGrasp-Anything) · [Paper](https://arxiv.org/abs/2503.08257)

<p align="center">
  <img src="../../../docs/assets/models/grasping/dexgrasp-anything-overview.png" alt="DexGrasp Anything overview and benchmark comparison" width="820" />
</p>

*Image source: official project repository.*

## Technical Summary

- **Problem:** Generate diverse, physically plausible high-DoF hand poses across many object categories.
- **Approach:** Conditional diffusion with physical constraints applied during training and sampling.
- **Primary hand:** Shadow Hand in the released experiments and dataset.
- **Venue:** CVPR 2025 Highlight.

## Physics-Aware Generation

DexGrasp Anything treats dexterous grasping as conditional generative modeling. Object geometry is encoded into semantic and spatial conditions, while the denoising process predicts hand configurations. Physical constraints guide the estimated clean pose during training and are applied again through a physics-guided sampler at inference time.

This design targets a recurring weakness of purely data-driven pose generation: a visually plausible hand configuration may penetrate the object, violate joint limits, or fail to establish stable contact. Physics guidance does not remove the need for simulator or real-world validation, but it moves these constraints into the generative process instead of relying only on post-filtering.

## Generation and Physical Evaluation

### Conditions and Physical Constraints

DexGrasp Anything predicts a high-dimensional hand configuration conditioned on object information. A diffusion model learns to transform a noisy pose into a grasp candidate through repeated denoising steps. Object geometry supplies the spatial condition; the project also explores semantic conditions for selecting a desired kind of grasp. The physical guidance acts on an estimated clean pose rather than treating every intermediate noisy state as a valid hand. This distinction matters because collision and contact quantities are meaningful only for geometrically interpretable configurations.

The guidance targets several constraints at once. Finger joints must remain within the hand's range; the hand should avoid penetrating the object or itself; contact should support a stable grasp rather than merely look close in an image. These objectives can conflict, so a generated pose is still a candidate that must be checked in simulation or on a robot. Diversity should be interpreted alongside validity: a method can produce many distinct poses while few of them are executable.

### Reading the Released Experiments

The dataset and evaluation code cover pose generation and physical testing, which should be kept distinct. In a cross-dataset comparison, confirm the object mesh or point-cloud preprocessing, hand coordinate convention, evaluation split, and whether physics-guided sampling was enabled. For real execution, the generated hand pose must also be converted to a reachable wrist trajectory and finger-control sequence; the model does not by itself perform approach planning or closed-loop recovery.

## Dataset and Cross-Dataset Evaluation

The project releases a dataset with more than 3.4 million grasp poses over more than 15,000 objects. It evaluates across DexGraspNet, UniDexGrasp, MultiDex, RealDex, and DexGRAB settings, using measures related to success, penetration, and diversity.

Those datasets differ in hand-pose conventions, object preprocessing, splits, and evaluation scripts. Reproduction should preserve coordinate transforms and clearly identify whether results use physics-guided sampling, LLM-derived conditions, or the base configuration.

## Reproduction Surface

The official repository provides source code, dataset links, checkpoints, training, sampling, and simulator-based testing. Its published setup uses Python 3.8, an older PyTorch/CUDA combination, PyTorch3D, CSDF, and Isaac Gym Preview 4. These dependencies are GPU- and version-sensitive.

The code repository declares an MIT license. Dataset and borrowed upstream assets should still be checked individually before redistribution.

## References

- [Official project page](https://dexgraspanything.github.io/)
- [Official repository](https://github.com/4DVLab/DexGrasp-Anything)
- [CVPR 2025 paper](https://arxiv.org/abs/2503.08257)
- [CVF open-access paper](https://openaccess.thecvf.com/content/CVPR2025/html/Zhong_DexGrasp_Anything_Towards_Universal_Robotic_Dexterous_Grasping_with_Physics_Awareness_CVPR_2025_paper.html)
