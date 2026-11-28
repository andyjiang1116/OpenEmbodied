# OpenWAM

[简体中文](openwam_ZH.md) · [World Action Models](README.md)

> **Research area:** World-Action Models · [Paper](https://arxiv.org/abs/2609.07398) · [Project](https://openwam-official.github.io/) · [Code](https://github.com/OpenWAM-Official/OpenWAM) · [Models and data](https://huggingface.co/OpenWAM)

OpenWAM is an open research stack for studying how a video-generative model can support robot action learning. The project distinguishes three contributions: **OpenWAM-Infra**, a modular implementation; **OpenWAM-Study**, controlled experiments on design choices; and **OpenWAM-α**, a pretrained world-action model. These names refer to a framework, an experimental study, and a model release, respectively, rather than three interchangeable policies.

## Research Problem

A world-action model connects predictions of how a scene evolves with predictions of what a robot should do. A video prior may supply knowledge about object motion and physical interactions, but that knowledge does not automatically become executable control. OpenWAM examines which representation, architecture, information-flow, and training choices make the transfer effective. Its modular implementation allows these choices to be varied within a shared training and evaluation stack.

## Method

OpenWAM-Infra separates the video backbone, visual representation, world-action architecture, attention pattern, training data, inference, and deployment configuration. The official repository provides configurations for several video backbones and visual encoders, along with dataset loaders and benchmark integrations. This design supports controlled comparisons of components without treating every configuration as a separate model family.

OpenWAM-Study investigates three connected questions: what knowledge to inherit from video pretraining, how world and action learning should interact, and how their combination scales with embodied data. The paper reports that useful transfer depends on a capable generative backbone and a compact informative latent representation. For world-action coupling, it identifies dedicated action capacity, explicit information flow from world features to action prediction, and synchronized joint denoising as important design choices. Its pretraining analysis emphasizes out-of-domain generalization and one-stage co-training with egocentric human video and robot data.

OpenWAM-α combines the selected design choices in a pretrained policy. The authors report pretraining on 518.5 million frames, approximately 6,400 hours, of egocentric human and robot data. This scale describes the authors' training corpus; it is not a requirement for fine-tuning a released checkpoint.

## Inputs, Outputs, and Deployment

The exact observation schema, action dimension, and preprocessing depend on the checkpoint and target embodiment. In the released workflow, a checkpoint includes its configuration and can be served as a policy over a WebSocket interface. A robot or benchmark client supplies observations and receives predicted actions. The official repository includes scripts for checkpoint download, fine-tuning, deployment, and single-request or continuous inference checks. It also includes benchmark data preparation for LIBERO, RoboTwin 2.0, RoboDojo, and other suites.

## Released Resources and Evaluation

The project publishes Apache-2.0 repository code, pretrained and fine-tuned checkpoints, data recipes, cleaned robot datasets, and evaluation protocols. The paper evaluates OpenWAM-α across eight simulation benchmarks and real-robot experiments spanning single-arm, bimanual, and dexterous-hand manipulation. These are results reported by the authors; the profile does not imply a common protocol or directly comparable scores across the other models in this collection.

For a first inspection, the official repository documents checkpoint download and a deployment path using `scripts/deploy.sh`. Its example training configuration uses a Wan2.2 video backbone and recommends eight 80 GB GPUs for training. Installation requires Python 3.10 or newer and a compatible PyTorch build. These resource and environment statements are specific to the published workflow and should be checked against the chosen configuration.

## Environment and Assets

The following commands run **inside a clone of the upstream OpenWAM repository** on a CUDA-capable Linux host. The official native installation uses Python 3.10 or newer, PyTorch 2.7.1 with CUDA 12.8 in its example, and an editable package install. Its Docker path is documented separately. Prepare the selected video backbone, benchmark dataset, and released checkpoint before training or serving; the repository's interactive downloaders can also be driven by flags for unattended use.

```bash
git clone https://github.com/OpenWAM-Official/OpenWAM.git
cd OpenWAM
conda create -n openwam python=3.10
conda activate openwam
pip install torch==2.7.1 torchvision==0.22.1 torchaudio==2.7.1 --index-url https://download.pytorch.org/whl/cu128
pip install -e .
python scripts/download_assets/download_benchmark_data.py
python scripts/download_assets/download_video_backbone.py
python scripts/download_assets/download_openwam_checkpoints.py
```

The benchmark and backbone downloaders require a selection. For the fine-tuning example below, select LIBERO and the **OpenWAM_Alpha / OpenWAM-Alpha-Pretrain-Foundation-Model** release. Record the resulting checkpoint directory. The pretrained checkpoint is distinct from the video backbone asset; a training configuration must resolve all component paths. The upstream [installation and assets guide](https://github.com/OpenWAM-Official/OpenWAM#installation) describes the alternatives and prerequisites.

## Fine-Tuning OpenWAM-α

The official LIBERO path initializes a new run from the foundation checkpoint:

```bash
bash scripts/train.sh \
  dataloader=libero \
  training.finetune_ckpt_path=<foundation_ckpt_dir_path>
```

Hydra composes `configs/train.yaml` with model, video-backbone, and dataloader groups. The LIBERO dataloader's `num_frames=33` and `video_stride=4` correspond to a 32-action horizon and nine sampled video frames; the checkpoint's model configuration and the dataloader's action dimensions, camera layout, transforms, and normalization must agree. For a new dataset or robot, change its dataloader and relevant model configuration rather than assuming the LIBERO preset provides the correct interface. The upstream [training and deployment guide](https://github.com/OpenWAM-Official/OpenWAM/blob/main/assets/openwam_usage_docs/train-and-deploy.md) documents component selection and CLI overrides.

`training.finetune_ckpt_path` loads model weights into a **new** run. `training.resume_ckpt_path` instead resumes a run with saved optimizer, scheduler, random-state, and model state; these fields are mutually exclusive. The official script detects visible GPUs and launches `torchrun`. The example with a Wan2.2 5B backbone recommends eight 80 GB GPUs for training; memory depends on architecture, frame count, batch size, and checkpointing settings. A short debug run can be launched with `training.debug=true` before a full training run.

## Checkpoint Serving and Client Integration

Deploy a released or fine-tuned checkpoint directory, which contains the resolved model configuration and associated assets:

```bash
bash scripts/deploy.sh <ckpt_dir_path>
```

The deploy script selects the newest checkpoint by default; `--ckpt-name <ckpt_file_name>` pins a specific file. Its default WebSocket server uses port 8848. The official inference helpers check one request and a continuous request stream:

```bash
python scripts/inference_test/inference_single_test.py \
  --server ws://127.0.0.1:8848 --test --state-dim 10
python scripts/inference_test/inference_continuous_test.py \
  --server ws://127.0.0.1:8848 --test --state-dim 10
```

These `--test` calls validate the service interface with synthetic input; they do not measure task success. The server handles `obs`, `reset`, and `ping` messages. Use the official [benchmark integration guide](https://github.com/OpenWAM-Official/OpenWAM/blob/main/assets/openwam_usage_docs/benchmark-integration.md) for payload fields and task clients. Match camera order, image resolution, proprioception width, action mapping, normalization, and temporal window before connecting a real robot. The deployment config controls denoising steps and modes, action-consumption horizon, video decoding, caches, and compilation; compilation can make the first request slower than steady-state inference.

## Relationship to Other World-Action Models

[Unified World Models](uwm.md) emphasizes a unified video-action diffusion model with separately controlled diffusion timesteps. [DreamZero](dreamzero.md) uses a pretrained video diffusion backbone for joint future-video and action generation. [Fast-WAM](fast-wam.md) uses video prediction during training while producing actions without explicit future-video generation at inference. OpenWAM's distinctive contribution is a modular experimental stack and a pretrained model built from the resulting design study. Comparisons should identify the exact checkpoint, backbone, observation and action interfaces, and evaluation protocol.

## References

- [OpenWAM paper](https://arxiv.org/abs/2609.07398)
- [Official project page](https://openwam-official.github.io/)
- [Official repository and implementation guide](https://github.com/OpenWAM-Official/OpenWAM)
- [Released models and data](https://huggingface.co/OpenWAM)
- [Training and deployment guide](https://github.com/OpenWAM-Official/OpenWAM/blob/main/assets/openwam_usage_docs/train-and-deploy.md)
- [OpenWAM-α fine-tuning guide](https://github.com/OpenWAM-Official/OpenWAM/blob/main/assets/openwam_usage_docs/openwam-alpha-finetuning.md)
