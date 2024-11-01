# 2024 Q0 OpenLAM Report

## Model Structure
- The DPA-2 model structure (PyTorch based) has been released, showing a significant increase in fitting and transferability compared to the DPA-1 (paper link: https://arxiv.org/abs/2312.15492).  
![图片](https://cdn1.deepmd.net/static/img/114d8a671280X1280-3.png)
- A new capability for unsupervised denoise pretraining has been added (https://doi.org/10.5281/zenodo.10483908).

## Data
- The DPA-2 paper includes pretrained data for 18 systems and downstream data for 10 systems, covering over ten million frames and 73 elements (for detailed data inventory, see below; data can also be directly downloaded from: https://doi.org/10.5281/zenodo.10483908).
- Four new datasets have been added for energy&force data related to electrolytes, solid-state electrolytes, chemical reactions, and methane combustion (for details, see the data inventory below).
- Seven new datasets in equilibrium state for unsupervised denoising tasks have been added, including AFLOW, MC2D/3D, CALYPSO, etc. (for details, see the data inventory below).

## Training Strategy
- The DPA-2 paper includes a multi-task pretraining framework for energy and force, supporting the combined training of datasets with different DFT settings.
- Unsupervised denoising task has been added, which is integrated into the multi-task pretraining framework (results are detailed below).

## Automation Process
- The DPA-2 paper encompasses an automated process for all stages of pretraining, fine-tuning, transferability testing, distillation, and compression (experience it at https://app.bohrium.dp.tech/dp-combo and try it on notebook: https://nb.bohrium.dp.tech/detail/18475433825).
- The AIS-Square website now includes an automated process for integrating user data (https://www.aissquare.com/openlam), automatically determining the coverage of the pretrained model on current data (https://github.com/zjgemi/lam-data-cleaning).

## Competition
Coming in March...

## Teaching
Coming in February...

Readers interested in the background of the project and details of the paper can also refer to the OpenLAM initiative (https://mp.weixin.qq.com/s/qfX7P32dKZ-VZgOtlYRy_A) and the DPA-2 paper (https://mp.weixin.qq.com/s/qy_t-eHdZ5nNf4L8i1sKfQ) for further information.

## Appendix
- Unsupervised Denoise Method
  - Data Structure
    - Equilibrium state data consisting only of configurations without DFT computational results; noise is added separately to the coordinates and types during preprocessing (such as adding Gaussian noise to coordinate positions and masking certain element types).
  - Training Method
    - Configurations with added noise are inputted into the network, processed by DPA-2's unified descriptor and denoise fitting, to yield a denoise vector for each atom (i.e., the network's prediction of the proper displacement) as well as the element types. After restoring the configuration and element types based on the denoise vector, a loss is computed against the true configurations and element types without noise. The model is trained by minimizing this loss.
- Data Inventory
  The datasets currently used for training the DPA-2 model cover a wide range of systems including semiconductors, perovskites, alloys, surface catalysis, cathode materials, solid-state electrolytes, organic molecules, and more. This includes the newly added unsupervised equilibrium state Denoise datasets. All these data have been uploaded to the AISSquare website [https://www.aissquare.com/], where users can find more detailed data descriptions, as well as download and use the datasets, specifically including:
  - Datasets included in the DPA-2 paper


Index|Dataset name|Contributors
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

  - Four new datasets for energy&force data

Index|Dataset name|Contributors
---|---|---
19|Electrolyte|Mengchao Shi, Yuzhi Zhang
20|Solid_State_Electrolyte|Mengchao Shi, Yuzhi Zhang
21|Organic_reactions_dataset|Tong Zhu, Bowen Li
22|CHO-methane-combustion|Jinzhe Zeng, Liqun Cao, Mingyuan Xu, Tong Zhu, John ZH Zhang

  - Seven new datasets in equilibrium state for unsupervised denoising

Index|Dataset name|Contributors/Link
---|---|---
1|AFLOW_MP|AFLOW：https://www.aflowlib.org/ MP：https://next-gen.materialsproject.org/
2|MC2D|Davide Campi, Nicolas Mounet, Marco Gibertini, Giovanni Pizzi, Nicola Marzari, The Materials Cloud 2D database (MC2D), Materials Cloud Archive 2022.84 (2022), doi: 10.24435/materialscloud:36-nd.
3|MC3D|Sebastiaan Huber, Marnik Bercx, Nicolas Hörmann, Martin Uhrin, Giovanni Pizzi, Nicola Marzari, Materials Cloud three-dimensional crystals database (MC3D), Materials Cloud Archive 2022.38 (2022), doi: 10.24435/materialscloud:rw-t0.
4|ChemicalSimilarity|Hai-Chen Wang, Silvana Botti, Miguel A. L. Marques, Finding new crystalline compounds using chemical similarity, Materials Cloud Archive 2021.68 (2021), doi: 10.24435/materialscloud:96-09.
5|ClusterIsomer|Giuseppe Fisicaro, Bastian Schaefer, Jonas A. Finkler, Stefan Goedecker, Principles of isomer stability in small clusters, Materials Cloud Archive 2023.36 (2023), doi: 10.24435/materialscloud:46-nr.
6|MolecularCrystal|Rose Cersonsky, Maria Pakhnova, Edgar Engel, Michele Ceriotti, Lattice energies and relaxed geometries for 2'707 organic molecular crystals and their 3'242 molecular components., Materials Cloud Archive 2023.5 (2023), doi: 10.24435/materialscloud:71-21.
7|CALYPSO_database|Zhenyu Wang, Xiaoshan Luo
  
- Latest Performance (RMSE error) of the Multi-task Pretrained Model (22 energy force systems + 7 unsupervised denoise systems)
![](https://cdn1.deepmd.net/static/img/a1baf4a2screenshot-20241031-143715.png)

Conclusion
Since the release of DPA-2 less than a month ago, there have been numerous developments that can be summarized as follows:
- The DPA-2 multitask pre-training framework has added a new unsupervised training task: it is now possible to train with any data derived from different DFT calculations together, as well as denoise equilibrium state data without DFT labels, thereby learning a broader range of representation information;
- The OpenLAM initiative has incorporated more production-type data and integrated more publicly available equilibrium state crystal structure data, with the pre-training data pool continuing to expand rapidly;
- After incorporating the unsupervised training task, the overall energy prediction accuracy of the model is higher when compared fairly, indicating that information across different systems and tasks promotes mutual enhancement.
The OpenLAM initiative is currently in rapid continuous iteration. As we move towards the era of large atomic models, open-source sharing becomes an inevitable theme. We welcome like-minded individuals to join, opening up new opportunities for broader scientific discoveries and industrial applications. On the journey to conquering the periodic table of elements, we look forward to creating a new era with you!
To join the "OpenLAM Initiative", visit: https://www.aissquare.com/openlam
