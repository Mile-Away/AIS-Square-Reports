# 2024 Q1 OpenLAM Report ｜ 基础设施升级、发布适配DeePMD-kit v3的预训练模型

## 代码

- 对代码进行了大规模重构: 3月初，DeePMD-kit v3 alpha版本顺利发布。相较于v2，DeePMD-kit v3允许用户在TensorFlow或PyTorch任意一个框架之上训练和运行深度势能模型，为拓宽下游生态提供了便利。DeePMD-kit v3还新增了对DPA-2模型的支持，翻开了大原子模型（LAM）的新篇章。更详细报告见：https://github.com/deepmodeling/deepmd-kit/discussions/3401。
- 在DeePMD-kit v3[最新的2024Q1分支版本](https://github.com/deepmodeling/deepmd-kit/tree/2024Q1)中，还包含了如下的新功能支持，主要包括：
  - DeepSpin升级：PyTorch版本现已支持包括DPA2在内的所有descriptor，可以结合如type embedding等模型结构，获得更高精度的磁性模型，为带磁性体系的研究推波助澜，输入案例见https://github.com/deepmodeling/deepmd-kit/blob/2024Q1/examples/spin/se_e2_a/input_torch.json 。
  - Multitask功能升级：PyTorch版本现已支持multitask finetune，允许用户基于预训练模型，同时在多个下游体系同时进行微调，文档见：https://github.com/deepmodeling/deepmd-kit/blob/devel/doc/train/finetuning.md#multi-task-fine-tuning。
## 数据

- 初步确定了[数据清洗的工作流](https://github.com/zjgemi/lam-data-cleaning)，并把[ColabFit 数据集](https://materials.colabfit.org/)中挑选的74个数据集纳入训练，测试表明在100任务量级的multitask训练中模型达到预期精度。
- 新增硫族固态电解质数据集，固态电解质数据覆盖了26种硫化物，相较于其他通用力场，DPA-SSE模型能更准确地预测动力学性质（如Li离子的扩散系数和离子电导率）。
- 对MPtraj数据集进行了清洗分类，并在更新后的DPA-2模型结构上进行训练测试，初步结果显示模型能力有提升。

## 模型

- 更新了与DeePMD-kit v3最新2024Q1分支版本适配的预训练模型 OpenLAM_2.1.0_27heads_20224Q1.pt，并上传至[AIS-Square网站](https://aissquare.com/models/detail?pageType=models&name=DPA-2.1.0-2024Q1&id=244)。测试表明，代码迁移至DeePMD-kit v3版本没有对模型精度产生影响。同时将包括ANI-1x, Transition-1x等此前作为下游测试集的任务加入了预训练模型中，并通过进行更充分的训练得到了更好的模型精度。
- 系统更新了zero-shot, single-task finetune, multitask-finetune等预训练模型的使用指南。对于模型使用有任何问问题，社区用户可在[GitHub讨论区](https://github.com/deepmodeling/deepmd-kit/discussions/3772)中 与开发者进行交流。

![模型](https://cdn1.deepmd.net/static/img/a861a163output.png)


## 基础设施

- [云原生AI4Science工作流框架Dflow](https://mp.weixin.qq.com/s/lyN3ZCfUiG38YEJW4KsCkg)开放和可扩展地推动的一系列社区软件生态发展。
  - 论文预印本：https://arxiv.org/abs/2404.18392
- dpgen2支持DeePMD-kit v3，并增加了面向DPA-2预训练模型调优的DP-Gen、大模型蒸馏工作流、面向多任务（multi-task）的DP-Gen等新特性。
  - 项目地址: https://github.com/deepmodeling/dpgen2
- [通过结合晶体结构预测算法CALYPSO与DP-Gen](https://mp.weixin.qq.com/s/697lWzw1-KOl6aA22IUgSg)，设计了适用于高通量结构预测模型的构建方案，并且将dpgen2嵌入结构搜索软件Calypso作为可选的构型空间探索引擎。
  - 文章地址：https://journals.aps.org/prb/abstract/10.1103/PhysRevB.109.094117
![图片](https://cdn1.deepmd.net/static/img/4944a86c1280X1280.PNG)
- 开源云原生合金性质计算工作流 APEX V1.2.0 发布，有效助力OpenLAM大原子模型评测。
  - 项目地址: https://github.com/deepmodeling/apex
  - 论文预印本：https://arxiv.org/abs/2404.17330
![图片](https://cdn1.deepmd.net/static/img/c46421d61280X1280-1.png)

## 社区

- OpenLAM交流会于三月顺利落幕。与会人员对OpenLAM的合作形式、短期目标、发展方向进行了充分交流并达成初步共识。
- 在北京科学智能研究院（AISI）的支持下，OpenLAM项目在本年度4-6月于北京举办集中的“[OpenLAM领域开发者训练营](https://mp.weixin.qq.com/s/tHpqqfiwpOlPfzaqqCJ4DA)”，围绕重点应用方向，以发布相应方向基本通用且ready to use的领域通用模型为阶段性目标，同步针对工作流开发、性质计算原理与实践、评估体系设计及开发，进行交流与培训。
