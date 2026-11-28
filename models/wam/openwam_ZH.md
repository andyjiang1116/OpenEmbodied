# OpenWAM

[English](openwam.md) · [世界动作模型](README_ZH.md)

> **研究方向：** 世界动作模型 · [论文](https://arxiv.org/abs/2609.07398) · [项目主页](https://openwam-official.github.io/) · [代码](https://github.com/OpenWAM-Official/OpenWAM) · [模型与数据](https://huggingface.co/OpenWAM)

OpenWAM 是研究视频生成模型如何支持机器人动作学习的开放式技术体系。项目包含三项不同性质的成果：模块化实现 **OpenWAM-Infra**、针对关键设计选择的对照研究 **OpenWAM-Study**，以及预训练世界动作模型 **OpenWAM-α**。三者分别对应研究框架、实验研究和模型发布，不能视为三个可互换的策略模型。

## 研究问题

世界动作模型将环境变化预测与机器人动作预测联系起来。视频预训练模型可能包含物体运动与交互知识，但这些知识不会自动转化为可执行的控制信号。OpenWAM 研究视觉表征、模型架构、信息流和训练数据的哪些设计选择有助于完成这种转化，并通过统一的训练与评测框架开展受控实验。

## 方法设计

OpenWAM-Infra 将视频骨干网络、视觉表征、世界动作架构、注意力模式、训练数据、推理及部署配置拆分为可组合模块。官方仓库提供多种视频骨干网络与视觉编码器的配置，也包含数据加载器和评测基准适配。这使不同组件能够在共享流程中比较，而无需把每种配置都视为独立的模型家族。

OpenWAM-Study 围绕三个问题展开：从视频预训练中继承什么知识，如何耦合世界建模与动作学习，以及两者结合后如何随具身数据规模变化。论文指出，有效的知识迁移依赖具备足够能力的视频生成骨干网络和紧凑、信息丰富的潜在表征。对于世界与动作的耦合，研究强调独立的动作建模能力、从世界表征到动作预测的显式信息流，以及同步的联合去噪。预训练分析重点考察分布外泛化，并采用第一人称人类视频与机器人数据的单阶段联合训练。

OpenWAM-α 将上述设计选择用于预训练策略。论文报告其训练数据包含 5.185 亿帧、约 6,400 小时的第一人称人类视频和机器人数据。该规模描述作者使用的预训练语料，不代表微调已发布权重所需的数据量。

## 输入输出与部署

具体观测格式、动作维度及预处理方式取决于 checkpoint 和目标机器人形态。官方流程中，每个已发布 checkpoint 自带配置，可通过 WebSocket 接口部署为策略服务；机器人或评测客户端发送观测，并接收预测动作。仓库提供权重下载、微调、部署、单次推理和连续推理检查脚本，同时支持 LIBERO、RoboTwin 2.0、RoboDojo 等评测基准的数据准备。

## 开放资源与评测

项目发布了采用 Apache-2.0 许可证的仓库代码，以及预训练与微调权重、数据配置、清洗后的机器人数据集和评测流程。论文在八项仿真评测及真实机器人实验中评估 OpenWAM-α，覆盖单臂、双臂和灵巧手操作。这里的性能结论来自原论文；不同项目若未统一 checkpoint、任务定义和评测协议，不宜直接比较分数。

官方仓库提供 checkpoint 下载和通过 `scripts/deploy.sh` 部署的流程。其示例训练配置采用 Wan2.2 视频骨干网络，建议使用 8 张各具 80 GB 显存的 GPU。安装说明要求 Python 3.10 或更高版本及兼容的 PyTorch。以上环境与资源要求对应官方发布流程，实际配置应以所选模型和实验设置为准。

## 环境与资源准备

以下命令需在支持 CUDA 的 Linux 主机、**OpenWAM 上游仓库克隆目录** 中执行。官方原生安装示例使用 Python 3.10 或更高版本、PyTorch 2.7.1 与 CUDA 12.8，并以可编辑模式安装项目；另有 Docker 部署路径。训练或部署前，应准备所选视频骨干网络、评测数据以及已发布权重。下载脚本默认提供交互式选择，也支持参数化运行。

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

下载数据和骨干网络时需选择相应资源。对于下文的微调示例，选择 LIBERO 数据，以及 **OpenWAM_Alpha / OpenWAM-Alpha-Pretrain-Foundation-Model** 权重，并记录下载后的 checkpoint 目录。预训练 checkpoint 与视频骨干网络资源不同，训练配置需能找到所有依赖的组件。其他安装方式及前提条件参见[官方安装与资源说明](https://github.com/OpenWAM-Official/OpenWAM#installation)。

## OpenWAM-α 微调

官方 LIBERO 流程从基础权重初始化一个新的训练实验：

```bash
bash scripts/train.sh \
  dataloader=libero \
  training.finetune_ckpt_path=<foundation_ckpt_dir_path>
```

Hydra 将 `configs/train.yaml` 与模型、视频骨干网络和数据加载器配置组合。LIBERO 数据加载器的 `num_frames=33`、`video_stride=4` 对应 32 步动作预测范围与 9 帧采样视频；checkpoint 的模型配置需要与数据加载器输出的动作维度、相机布局、数据变换和归一化保持一致。接入新数据集或机器人时，应调整数据加载器和相关模型配置，不能直接沿用 LIBERO 的接口。组件选择和命令行覆盖方式参见[官方训练与部署说明](https://github.com/OpenWAM-Official/OpenWAM/blob/main/assets/openwam_usage_docs/train-and-deploy.md)。

`training.finetune_ckpt_path` 仅加载模型权重，并开始新的训练实验；`training.resume_ckpt_path` 用于恢复包含优化器、学习率调度器、随机状态和模型状态的完整训练记录。两项配置互斥。官方脚本检测可见 GPU 并通过 `torchrun` 启动。使用 Wan2.2 5B 骨干网络的示例建议 8 张各具 80 GB 显存的 GPU；实际需求随架构、帧数、批量大小和梯度检查点设置变化。正式训练前可用 `training.debug=true` 进行短流程检查。

## 权重服务与客户端接入

已发布权重或微调结果均可通过 checkpoint 目录部署，目录中包含解析后的模型配置及相关资源：

```bash
bash scripts/deploy.sh <ckpt_dir_path>
```

部署脚本默认选择最新的 checkpoint；使用 `--ckpt-name <ckpt_file_name>` 可指定文件。默认 WebSocket 服务端口为 8848。官方提供单次请求与连续请求检查脚本：

```bash
python scripts/inference_test/inference_single_test.py \
  --server ws://127.0.0.1:8848 --test --state-dim 10
python scripts/inference_test/inference_continuous_test.py \
  --server ws://127.0.0.1:8848 --test --state-dim 10
```

上述 `--test` 命令使用模拟输入检查服务接口，不能代表任务成功率。服务端处理 `obs`、`reset` 和 `ping` 消息；具体数据字段和评测客户端参见[官方基准接入说明](https://github.com/OpenWAM-Official/OpenWAM/blob/main/assets/openwam_usage_docs/benchmark-integration.md)。连接真实机器人前，应校对相机顺序、图像分辨率、本体状态维度、动作映射、归一化以及时间窗口。部署配置还控制去噪步数与模式、动作片段消耗长度、视频解码、缓存和编译；首次请求可能包含编译预热延迟。

## 与其他世界动作模型的关系

[Unified World Models](uwm_ZH.md) 侧重具有独立扩散时间步控制的视频与动作联合扩散模型。[DreamZero](dreamzero_ZH.md) 借助预训练视频扩散骨干网络，联合生成未来视频与动作。[Fast-WAM](fast-wam_ZH.md) 在训练中引入视频预测，推理时无需显式生成未来视频。OpenWAM 的特点是模块化实验框架，以及基于系统设计研究构建的预训练模型。横向比较时，应明确 checkpoint、视频骨干网络、观测与动作接口及评测协议。

## 参考资料

- [OpenWAM 论文](https://arxiv.org/abs/2609.07398)
- [官方项目主页](https://openwam-official.github.io/)
- [官方代码与实现说明](https://github.com/OpenWAM-Official/OpenWAM)
- [已发布模型与数据](https://huggingface.co/OpenWAM)
- [训练与部署说明](https://github.com/OpenWAM-Official/OpenWAM/blob/main/assets/openwam_usage_docs/train-and-deploy.md)
- [OpenWAM-α 微调说明](https://github.com/OpenWAM-Official/OpenWAM/blob/main/assets/openwam_usage_docs/openwam-alpha-finetuning.md)
