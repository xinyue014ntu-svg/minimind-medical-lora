# 🏥 MiniMind-Medical-LoRA: 基于垂直领域知识的大模型微调实践

![Python](https://img.shields.io/badge/Python-3.10%2B-blue)
![PyTorch](https://img.shields.io/badge/PyTorch-2.0%2B-red)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📖 项目简介
本项目基于轻量级大语言模型架构（MiniMind），完整跑通了从 **指令微调 (SFT)** 到 **垂直领域低秩微调 (LoRA)** 的大模型全生命周期训练链路。核心目标是探索在有限算力下，如何通过参数高效微调（PEFT）技术，将一个通用语言模型改造为具备专业医学知识的垂直领域问答助手。

## ✨ 核心工程亮点 (Engineering Highlights)
* **全链路跑通**：独立完成了环境配置、数据集拉取（ModelScope）、SFT 全量指令微调及多组 LoRA 权重训练。
* **认知微调 (Identity Alignment)**：使用自我认知数据集进行极速 LoRA 微调（150 Epochs），成功将模型底层思想钢印替换为定制化身份。
* **攻克“灾难性遗忘” (Catastrophic Forgetting)**：
  * **问题复现**：在初始医疗数据微调中，模型出现严重的语言能力崩坏（如输出“牙疼是由鳄鱼引起”等乱码逻辑）。
  * **问题解决**：通过深入分析，判定为过拟合导致的基础语言结构破坏。随后通过动态调整超参数（将 Epochs 降至 3-5，Learning Rate 调优至 `5e-5`），成功在“注入新知识”与“保留原有语言能力”之间找到平衡点。

## 🛠️ 技术栈
* **算法架构**：Transformer (Causal LM), LoRA
* **框架与工具**：PyTorch, Transformers, ModelScope
* **开发环境**：AutoDL (Linux), JupyterLab

## 🚀 快速开始 (Quick Start)

###  准备环境
```bash
git clone [https://github.com/xinyue014ntu-svg/minimind-medical-lora.git](https://github.com/xinyue014ntu-svg/minimind-medical-lora.git)
cd minimind-medical-lora

###⚠️ 提示：受限于 GitHub 文件大小限制，本项目未直接上传几百 MB 的 .pth 权重文件。如需测试，请先按文档拉取数据集并运行 trainer/train_lora.py 在本地生成对应的 LoRA 权重。
