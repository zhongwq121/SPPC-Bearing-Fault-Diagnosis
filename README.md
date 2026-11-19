# SPPC: Selective Physics-Based Prediction Correction

**Selective Physics-Based Prediction Correction for Cross-Machine Bearing Fault Diagnosis**

*A training-free, post-hoc approach to correcting inner-race/outer-race fault confusion using bearing-specific physical evidence.*

> ⚠️ **Release Status:** This repository currently serves as a project overview. The source code, pre-trained weights, and reproduction instructions are being organized and will be officially released upon the acceptance of the manuscript. 

## 📖 Overview

Deep learning models for bearing fault diagnosis can struggle when deployed on machines that differ from those seen during training. A particularly important error occurs when a model correctly identifies a faulty bearing but confuses an **inner-race fault (Inner)** with an **outer-race fault (Outer)**.

SPPC addresses this fault-location confusion **after** a diagnostic model has made its prediction. Rather than retraining the model or replacing its three-class decision, SPPC uses an independent signal-processing branch to determine whether the predicted fault location should be revised. The original prediction is retained whenever the required physical information is unavailable or the physical decisions are inconsistent.

## 🧠 Method

SPPC combines three key elements:

1. **Bearing-specific physical evidence.** Given validated bearing geometry and a usable speed/angle reference, SPPC constructs an envelope order spectrum and evaluates candidate bands around the BPFI and BPFO harmonics. Band-averaged spectral amplitudes reduce the scoring bias caused by different numbers of spectral bins.
2. **Multi-harmonic comparisons.** Physical evidence is accumulated across harmonics, with decisions evaluated at the fixed prefix set **K = {1, 2, 4, 8, 12}**.
3. **Selective correction.** A physical decision can replace the original Inner/Outer prediction only when the required physical-information conditions hold and all five prefix decisions agree. Otherwise, the original prediction is retained. Predictions of **Normal** are strictly preserved.

## 📊 Experimental Evaluation

We evaluate SPPC in two distinct settings:

| Evaluation | Datasets / Model | Main Result |
| :--- | :--- | :--- |
| **Development & Analysis** | CWRU, UOTTAWA, MFPT, DZLRSB; six frozen backbones | Mean accuracy across four domains and six backbones: **65.39% → 92.82%** |
| **Independent Validation** | Paderborn; frozen CDDG backbone | Class-balanced, bearing-equal window accuracy: **40.13% → 42.87%** |

The development datasets were used to establish the method. **Paderborn was strictly reserved for validation after the SPPC rules and parameters were fixed.**

## 💻 Code and Data Availability

*   **Code:** The SPPC implementation is **not yet available** in this repository. The release is intended to include the physical correction module, experiment configurations, and instructions for reproducing the results. This section will be updated when materials are ready.
*   **Data:** The bearing datasets (CWRU, UOTTAWA, MFPT, DZLRSB, Paderborn) are provided by their original maintainers and are not redistributed here.

## 📝 Paper and Citation

**Manuscript:** *Selective Physics-Based Prediction Correction for Cross-Machine Bearing Fault Diagnosis*

The paper link and BibTeX citation will be added when the manuscript is publicly available.

## 📄 License

The source code of this project will be open-sourced under the **MIT License** upon official release.

---
<details>
<summary><b>🇨🇳 点击查看中文版说明 (Click to view Chinese Version)</b></summary>

# SPPC：基于物理证据的选择性预测修正

**跨机器轴承故障诊断中基于物理证据的选择性预测修正**

*一种免训练、基于后处理的方法，利用轴承特定的物理证据来修正内圈/外圈故障混淆。*

> ⚠️ **发布状态**：当前仓库仅作为项目概述。源代码、预训练模型及复现指南正在整理中，将在论文录用后正式开源。

## 📖 概述
用于轴承故障诊断的深度学习模型在部署到未见过的机器上时，往往会面临性能下降。一种尤为关键的误差是：模型虽然正确识别了轴承故障，却将**内圈故障 (Inner)** 与 **外圈故障 (Outer)** 混淆。SPPC 在模型做出预测**之后**进行修正。它不重新训练模型，也不改变原有的三分类决策，而是利用独立的信号处理分支来决定是否修正预测位置。当缺乏物理信息或判断不一致时，保留原预测。

## 🧠 方法
SPPC 结合了三个关键要素：
1. **轴承特定的物理证据**：构建包络阶次谱，并评估 BPFI/BPFO 谐波附近的候选频带。频带平均谱幅值消除了谱点数差异带来的偏置。
2. **多谐波对比**：在固定的前缀集合 **K = {1, 2, 4, 8, 12}** 下累积物理证据。
3. **选择性修正**：仅当物理信息条件满足且五个前缀判断完全一致时，才允许替换原始预测。**正常 (Normal)** 类别的预测绝不被改变。

## 📊 实验评估
| 评估场景 | 数据集 / 模型 | 主要结果 |
| :--- | :--- | :--- |
| **开发与分析** | CWRU, UOTTAWA, MFPT, DZLRSB；六种冻结骨干 | 平均准确率：**65.39% → 92.82%** |
| **独立外部验证** | Paderborn；冻结的 CDDG 骨干模型 | 类别平衡等权准确率：**40.13% → 42.87%** |

## 💻 代码与数据
*   **代码**：尚未发布，发布内容将包含修正模块及复现指南。
*   **数据**：原始数据集由各维护者提供，本仓库不重新分发。

## 📝 引用
论文链接及 BibTeX 将在论文公开后添加。

## 📄 许可证
正式发布时，源代码将采用 **MIT License** 开源。

</details>
