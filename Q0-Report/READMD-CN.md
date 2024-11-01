# 2024 Q0 Report

## 详细Report
在迈向通用大原子模型 (Large Atomic Model，LAM) 的征途上，深度势能核心开发者团队面向社区，发起 OpenLAM 大原子模型计划。OpenLAM 的口号是“征服元素周期表！”，希望通过建立开源开放的围绕微尺度大模型的生态，为微观科学研究提供新的基础设施，并推动材料、能源、生物制药等领域微尺度工业设计的变革。
“大原子模型计划(OpenLAM)”为进一步打破数据壁垒，拓宽原子层面各方面的应用，为开源开放的科学计算生态共建打开了新的思路。2023年底，深度势能团队面向社区发布了深度势能预训练大模型DPA-2，将成为OpenLAM大原子模型计划的重要载体。基于DPA-2的微调/蒸馏/应用自动化流程也于同期面向社区全面开放，打通了面向各类实际应用的最后一公里。相关文章[1]以《DPA-2: Towards a universal large atomic model for molecular and material simulation》为题，在arXiv上预发表 https://arxiv.org/abs/2312.15492  
  ![图片](https://cdn1.deepmd.net/static/img/ce9e64621280X1280-2.png "https://arxiv.org/abs/2312.15492")

自此，OpenLAM将进入快速迭代、协作的周期，深度势能团队将会每3个月会发布版本更新报告，本次报告作为2024 Q0的发布总结，点击原文跳转原blog (https://deepmodeling.com/blog/openlam-2024Q0/) ，以下是报告的主要内容：
## 模型结构
- DPA-2 模型结构 (PyTorch based) 发布，相比DPA-1本身拟合能力、迁移能力大幅提升 (paper link: https://arxiv.org/abs/2312.15492) 
![图片](https://cdn1.deepmd.net/static/img/114d8a671280X1280-3.png)
- 新增无监督denoise预训练能力 (https://doi.org/10.5281/zenodo.10483908) 
## 数据
- DPA-2 paper中包含的预训练18个体系以及下游10个体系数据，超千万帧数据覆盖73种元素 (详细见下文数据清单，也可以直接打包下载：https://doi.org/10.5281/zenodo.10483908) 
- 新增电解液、固态电解质、化学反应和甲烷燃烧4个能量受力数据集 (详细见下文数据清单) 
- 新增AFLOW、MC2D/3D、CALYPSO等7个无监督稳定结构数据集 (详细见下文数据清单) 
## 训练策略
- DPA-2 paper中所包含的能量受力多任务预训练框架，支持不同DFT label方式数据集放在一起训练
- 新增无监督denoise任务，共同加入多任务预训练框架 (效果见下文结果) 
## 自动化流程
- DPA-2 paper中所包含的所有预训练、微调、迁移性测试、蒸馏、压缩自动化流程 (可以在https://app.bohrium.dp.tech/dp-combo 体验， notebook: https://nb.bohrium.dp.tech/detail/18475433825) 
- AIS-Square网站用户数据自动化纳入流程 (https://www.aissquare.com/openlam) ，自动判断预训练模型对当前数据的迁移覆盖程度 (https://github.com/zjgemi/lam-data-cleaning) 
## 比赛
三月即将推出。。。
## 教学
二月即将推出。。。


关于项目的背景和论文细节介绍，感兴趣的读者也可以参考OpenLAM计划 (https://mp.weixin.qq.com/s/qfX7P32dKZ-VZgOtlYRy_A) 和DPA-2 paper (https://mp.weixin.qq.com/s/qy_t-eHdZ5nNf4L8i1sKfQ) 相关推送。

## 附录：
- 无监督denoise方式说明
  - 数据结构
    - 均衡态数据，仅构型，无DFT计算结果；预处理时对坐标和类型分别加noise (如对坐标位置加gaussian噪声、对部分元素类型进行mask) ；
  - 训练方式
    - 向网络输入加完noise的构型，经过DPA-2的unified descriptor和denoise fitting，得出每个原子的denoise vector (即网络预测的应有的偏移) 以及元素类型，对构型和元素类型进行恢复后，和真实未加noise的构型和元素类型做loss，最小化loss训练模型即可。
- 数据清单
  目前用于训练DPA-2模型的数据集已覆盖了半导体，钙钛矿，合金，表面催化，正极材料，固态电解质，有机分子等多类体系，包括新增的无监督稳定结构数据集，这些数据均已上传到aissquare网站[https://www.aissquare.com/]，用户可以在网站上查看更详细的数据说明，以及下载和使用，具体包括：
  - DPA-2 paper中包含的数据集

序号|数据集名称|贡献者
---|---|---
1|Alloy_DPA_v1_0|Fuzhi Dai, Wanrun Jiang
2|Cathode(Anode)_DPA_v1_0|Linshuang Zhang, Jianchuan Liu
3|Cluster_DPA_v1_0|Fuqiang Gong
4|Drug(drug-like-molecule)_DPA_v1_0|Manyi Yang
5|FerroEle_DPA_v1_0|Jing Wu, Jiyuan Yang, YuanJinsheng Liu, Duo Zhang, Yudi Yang, Yuzhi Zhang, Linfeng Zhang, Shi Liu
6|Open_Catalyst_2020(OC20_Dataset)|Duo Zhang
7|SSE-PBE_DPA_v1_0|Jianxing Huang
8|SemiCond_DPA_v1_0|Jianchuan Liu
9|H2O-PD_DPA_v1_0|Linfeng Zhang, Han Wang, Roberto Car, Weinan E
10|AgAu-PBE(unitary)_DPA_v1_0|Yinan Wang, LinFeng Zhang, Ben Xu, Xiaoyang Wang, Han Wang
11|AlMgCu_DPA_v1_0|Wanrun Jiang, Yuzhi Zhang, Linfeng Zhang, Han Wang
12|Cu_DPA_v1_0|Yuzhi Zhang, Haidi Wang, Weijie Chen, Jinzhe Zeng, Linfeng Zhang
13|Sn_DPA_v1_0|Fengbo Yuan
14|Ti_DPA_v1_0|Tongqi Wen, Rui Wang, Lingyu Zhu, Linfeng Zhang, Han Wang, David J Srolovitz, Zhaoxuan Wu
15|V_DPA_v1_0|Rui Wang, Xiaoxiao Ma, Linfeng Zhang, Han Wang, David J Srolovitz, Tongqi Wen, Zhaoxuan Wu
16|W_DPA_v1_0|Xiaoyang Wang, Yinan Wang, Linfeng Zhang, Fuzhi Dai, Han Wang
17|C12H26_DPA_v1_0|Jinzhe Zeng, Linfeng Zhang, Han Wang, Tong Zhu
18|HfO2_DPA_v1_0|Jing Wu, Yuzhi Zhang, Linfeng Zhang, Shi Liu
  - 新增4个能量受力数据集

序号|数据集名称|贡献者
---|---|---
19|Electrolyte|Mengchao Shi, Yuzhi Zhang
20|Solid_State_Electrolyte|Mengchao Shi, Yuzhi Zhang
21|Organic_reactions_dataset|Tong Zhu, Bowen Li
22|CHO-methane-combustion|Jinzhe Zeng, Liqun Cao, Mingyuan Xu, Tong Zhu, John ZH Zhang

  - 新增7个无监督稳定结构数据集

序号|数据集名称|贡献者/索引
---|---|---
1|AFLOW_MP|AFLOW：https://www.aflowlib.org/ MP：https://next-gen.materialsproject.org/
2|MC2D|Davide Campi, Nicolas Mounet, Marco Gibertini, Giovanni Pizzi, Nicola Marzari, The Materials Cloud 2D database (MC2D), Materials Cloud Archive 2022.84 (2022), doi: 10.24435/materialscloud:36-nd.
3|MC3D|Sebastiaan Huber, Marnik Bercx, Nicolas Hörmann, Martin Uhrin, Giovanni Pizzi, Nicola Marzari, Materials Cloud three-dimensional crystals database (MC3D), Materials Cloud Archive 2022.38 (2022), doi: 10.24435/materialscloud:rw-t0.
4|ChemicalSimilarity|Hai-Chen Wang, Silvana Botti, Miguel A. L. Marques, Finding new crystalline compounds using chemical similarity, Materials Cloud Archive 2021.68 (2021), doi: 10.24435/materialscloud:96-09.
5|ClusterIsomer|Giuseppe Fisicaro, Bastian Schaefer, Jonas A. Finkler, Stefan Goedecker, Principles of isomer stability in small clusters, Materials Cloud Archive 2023.36 (2023), doi: 10.24435/materialscloud:46-nr.
6|MolecularCrystal|Rose Cersonsky, Maria Pakhnova, Edgar Engel, Michele Ceriotti, Lattice energies and relaxed geometries for 2'707 organic molecular crystals and their 3'242 molecular components., Materials Cloud Archive 2023.5 (2023), doi: 10.24435/materialscloud:71-21.
7|CALYPSO_database|Zhenyu Wang, Xiaoshan Luo

- 最新多任务预训练模型结果RMSE (22 能量受力体系+7 无监督稳定结构体系)  
![](https://cdn1.deepmd.net/static/img/994eea1fscreenshot-20241031-140458.png)

总结
在DPA-2发布至今不到一个月的时间里，又有了上述较多进展，可以总结如下：
- DPA-2多任务预训练框架新增无监督训练支持：不仅可以将不同DFT计算数据放在一起训练，也可以对无DFT标注的稳定结构数据进行无监督训练，从而学到更广泛的表示信息；
- OpenLAM计划新增了更多生产型数据，以及纳入了更多公开的稳定结构数据，预训练数据池还在不断迅速扩大；
- 加入无监督训练任务后，模型依然能稳定拟合，而且在公平比较的情况下，模型整体的能量预测精度会更高，说明不同体系、不同任务之间的信息有互相促进。
OpenLAM计划目前正在持续快速迭代中，在走向大原子模型时代的过程中，开源开放将是必然的主题。欢迎志同道合的各位加入，开启更广泛科学发现和工业应用的新机遇。在征服元素周期表的路上，期待与你携手共创！
前往加入”大原子模型计划”： https://www.aissquare.com/openlam

