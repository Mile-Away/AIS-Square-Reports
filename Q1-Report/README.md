
# 2024 Q1 OpenLAM Report | Infrastructure Upgrades, Pre-trained Models for DeePMD-kit v3 Released

## Code
- A large-scale refactoring of the code was carried out. In early March, DeePMD-kit v3 alpha version was successfully released Compared with v2, DeePMD-kit v3 allows users to train and run deep potential energy models on either TensorFlow or PyTorch framework, providing convenience for expanding downstream ecosystems. DeePMD-kit v3 also adds support for DPA-2 models, opening a new chapter for large atomic models (LAM) . For more detailed report, see: https://github.com/deepmodeling/deepmd-kit/discussions/3401
- In [the latest 2024Q1 branch version](https://github.com/deepmodeling/deepmd-kit/tree/2024Q1) of DeePMD-kit v3, the following new feature support is also included, mainly including:
  - DeepSpin upgrade, PyTorch version now supports all descriptors including DPA2, which can be combined with model structures such as type embedding to obtain higher precision magnetic models, which promotes the study of magnetic systems. See https://github.com/deepmodeling/deepmd-kit/blob/2024Q1/examples/spin/se_e2_a/input_torch.json for input cases.
  - Multitask function upgrade, PyTorch version now supports multitask finetune, allowing users to fine-tune multiple downstream systems simultaneously based on pre-trained models, see: https://github.com/deepmodeling/deepmd-kit/blob/devel/doc/train/finetuning.md#multi-task-fine-tuning .
## Data
- Preliminary determination of the data cleaning workflow ( https://github.com/zjgemi/lam-data-cleaning ), and the ColabFit dataset ( https://materials.colabfit.org/ ) selected in the 74 datasets into training, testing shows that in the 100-level multitask training model to achieve the expected accuracy.
- Added chalcogenide solid electrolyte dataset, the solid electrolyte data covers 26 sulfides. Compared with other general force fields, the DPA-SSE model can more accurately predict kinetic properties (such as the diffusion coefficient and ionic conductivity of Li ions).
- The MPtraj dataset was cleaned and classified, and trained and tested on the updated DPA-2 model structure. Preliminary results show that the model's ability has improved.
## Model

- Updated the pre-trained model OpenLAM_2. 0_27heads_20224Q1.pt adapted to the latest 2024Q1 branch version of DeePMD-kit v3 and uploaded it to the AIS-Square website https://aissquare.com/models/detail?pageType=models&name=DPA-2.1.0-2024Q1&id=244 . Tests show that the code migration to DeePMD-kit v3 has no impact on the model accuracy. At the same time, tasks such as ANI-1x and Transition-1x, which were previously used as downstream test sets, were added to the pre-trained model, and better model accuracy was obtained through more comprehensive training.
- The system has updated the user guide for pre-trained models such as zero-shot, single-task finetune, and multitask-finetune. If you have any questions about the use of the model, community users can https://github.com/deepmodeling/deepmd-kit/discussions/3772 communicate with developers in the GitHub discussion area.
![模型](https://cdn1.deepmd.net/static/img/a861a163output.png)

## Infrastructure
- Cloud Native AI4Science workflow framework Dflow open and scalable to promote a series of community software ecosystem development.
  - Paper preprint : https://arxiv.org/abs/2404.18392
- Dpgen2 supports DeePMD-kit v3 and adds new features such as DP-Gen for DPA-2 pre-trained model tuning, large model distillation workflow, and DP-G EN for multi-task .
  - Project address: https://github.com/deepmodeling/dpgen2
- By combining crystal structure prediction algorithms CALYPSO and DP-GEN , a construction scheme suitable for high-throughput structure prediction models is designed, and dpgen2 is embedded in structure search software Calypso as an optional configuration space exploration engine.
  - Article address: https://journals.aps.org/prb/abstract/10.1103/PhysRevB.109.094117
![图片](https://cdn1.deepmd.net/static/img/4944a86c1280X1280.PNG)

- The open-source Cloud Native alloy property calculation workflow APEX V1.2.0 has been released, effectively assisting in the evaluation of OpenLAM large atomic models.
  - Project address: https://github.com/deepmodeling/apex
  - Preprints of papers: https://arxiv.org/abs/2404.17330
![图片](https://cdn1.deepmd.net/static/img/c46421d61280X1280-1.png)

## Community
- The OpenLAM exchange meeting ended successfully in March. Participants fully exchanged views on the cooperation form, short-term goals, and development direction of OpenLAM and reached preliminary consensus.
- With the support of the Beijing Institute of Scientific Intelligence (AISI), the OpenLAM project held a centralized " OpenLAM Field Developer Training Camp " in Beijing from April to June this year. Focusing on key application directions, the project aims to release domain-specific models that are basically universal and ready to use in the corresponding directions. It also conducts communication and training on workflow development, property calculation principles and practices, evaluation system design and development.


