# 2024 Q2 OpenLAM Report | More Robust Code, More Domain-specific Models

## Code
- DeePMDkit-v3-beta version (v3.0.0b3) released . Compared to the earlier released alpha version, the beta version has a more complete refactoring of the code, more comprehensive support for various model modules, optimized DPA2 model support for LAMMPS, and added more new features. v3.0.0b3 version further fixed known bugs in v3.0.0b0 , v3.0.0b1 and v3.0.0b2, and passed systematic testing. A DPA2 pre-trained model compatible with v3.0.0b3 (see below) has been released, detailes on supported features and optimization can be found in the release note:
  - https://github.com/deepmodeling/deepmd-kit/releases/tag/v3.0.0b0
  - https://github.com/deepmodeling/deepmd-kit/releases/tag/v3.0.0b1
  - https://github.com/deepmodeling/deepmd-kit/releases/tag/v3.0.0b2 
  - https://github.com/deepmodeling/deepmd-kit/releases/tag/v3.0.0b3 (recommended)
- ABACUS software version 3.7 released. The new version of ABACUS has been comprehensively tested for the alloy field to ensure the accuracy and pseudopotential reliability of the calculation. At the same time, in order to support the OpenLAM large atomic model plan, it has been deeply optimized to improve the performance on domestic DCU hardware, including memory utilization efficiency and calculation speed, further expanding its application scope in first-principles label calculation of large atomic models. See  https://mp.weixin.qq.com/s/oAFKJzhjV1eghaYTqiWUbQ

## Data
- High-pressure hydrogen-rich compound data
  - A high-pressure hydrogen-rich compound database containing 140,000 data, 29-element ternary hydrogen-rich compounds, covering a pressure range of 150-250 GPa. Data link: https://www.aissquare.com/datasets/detail?pageType=datasets&name=High-Pressure-Hydrogen-Rich-Compound&id=257
- Solid-state electrolyte data (SSE-ABACUS)
  - Contains 127,000 data, 27 elements, 365 systems (including sulfides, halides, doping and interfaces). Data link: https://www.aissquare.com/datasets/detail?pageType=datasets&name=SSE-abacus&id=260
## Model
- Pre-trained model based on DeepMDkit-v3-beta version
  - Updated multi-task DPA-2 pre-trained model compatible with DeePMD-kit-beta version (v3.0.0b3 )  https://www.aissquare.com/models/detail?pageType=models&name=DPA-2.2.0-beta3&id=272
  - And DPA-2 single-task pre-trained models

Dataset|Dataset card|Model card
------------|--------------|------------
SSE-ABACUS|https://www.aissquare.com/datasets/detail?name=SSE-abacus&id=260&pageType=datasets|https://www.aissquare.com/models/detail?pageType=models&name=SSE-ABACUS-dpa2&id=267
SSE-VASP|https://www.aissquare.com/datasets/detail?name=Solid_State_Electrolyte&id=217&pageType=datasets|https://www.aissquare.com/models/detail?pageType=models&name=SSE-VASP-dpa2&id=266
Electrolyte|https://www.aissquare.com/datasets/detail?name=Electrolyte&id=216&pageType=datasets|https://www.aissquare.com/models/detail?pageType=models&name=Electrolyte-dpa2&id=268

- Domain models
  - Free Energy Pertubation Model  (https://arxiv.org/pdf/2406.09817) 
    - On NNP, using DPA-2 and semi-empirical method to achieve accuracy equivalent to DFT.
    - A new NNP tuning molecular force field pipeline was designed, while ensuring the accuracy of the potential energy surface at the NNP level and the calculation efficiency at the MM level.
  - Solid state battery
    - A large pre-trained model of solid electrolyte, DPA-SSE ( SSE-ABACUS dataset), was constructed. The energy accuracy predicted by the model is an order of magnitude higher than that of CHGNET and M3GNET, and the force accuracy is improved by 1-5 times. In terms of dynamic properties, the diffusion coefficient and conductivity of Li ions predicted by DPA-SSE have good consistency with the experiments.
    - Pre-trained model of bulk materials (cholerates), online to arXiv ( http://arxiv.org/abs/2406.18263 )
    - Dedicated app for developing pre-trained models for solid electrolytes ( https://bohrium.dp.tech/apps/voltcraft )
  - Alloy
    - A pre-trained large atomic model of the alloy containing 53 elements was constructed, and first-principles calculations were performed using domestic ABACUS software and DCU machines to generate 24,000 data. The configurations include elemental, compound, high-entropy alloy crystal structures, vacancy, self-interstitial, surface defect structures, etc. The pressure range is - 0.5-5 GPa, and the temperature range is 50-3000 K. The energy accuracy of the trained model can be less than 35 meV/atom, and the force accuracy can be less than 0.25 eV/Å.
    - Compared with the existing MACE pre-trained large atomic model, the developed alloy domain model performs better in properties such as elastic constant, modulus, surface energy, and point defect formation energy.
  - High pressure hydrogen rich compound
    - An atomic-scale model suitable for predicting the structure of high-pressure hydrogen-rich superconducting compounds (including 152702 datasets, 29 elements of ternary hydrogen-rich compounds, covering a pressure range of 150-250 GPa) was constructed.
    - The DPA-1 model is based on the 2024Q1 version and can currently stably optimize the structures of 28 known hydrogen-rich superconducting compounds, and the spatial groups before and after optimization are consistent. ( https://www.aissquare.com/models/detail?pageType=models&name=High-Pressure-Hydrogen-Rich-Compound&id=258 )
  - Dynamic catalysis
    - A general potential function model for dynamic catalytic elementary reactions on cluster surfaces, DPA-DynaCat,  was constructed. The training dataset includes common small molecule-related elementary reactions such as $H_2$/$O_2$/$H_2O$/$CO$/$CO_2$/$CH_4$ occurring on the surface of $Au/Ag/Cu/Pt/Pd/Ni$ pure metals and binary alloy clusters.
    - Compared with the results of DFT calculation, the model can accurately predict the potential energy surface, and can obtain an approximated free energy of reaction in contrast to machine Learning potential models for a single system. This model can be combined with molecular dynamics for enhanced sampling, considering the contribution of each isomer in the reaction process, and can be used to calculate the reaction energy barrier and free energy of . ( https://www.aissquare.com/models/detail?pageType=models&name=DPA-DynaCat&id=262 )

## Community
-  The LAM Crystal Philately Competition officially kicked off on July 1st. This will be a long-term competition aimed at providing a testing and polishing platform for crystal structure search and generation algorithms, while providing a richer chemical space for OpenLAM updates. See ( https://bohrium.dp.tech/competitions/8821838186?tab=introduce ) for details.
- Based on the Crystal Structure Philately Competition, the OPENLAM crystal structure database has been constructed, which currently includes more than 500,000 stable structures. All structures in the database can be accessed through the official API ( https://github.com/deepmodeling/openlam ); In order to promote the effective connection between the language and perspective of experimental scientists and the current artificial intelligence technology and database progress, we have developed the Crystal Craft APP ( https://bohrium.dp.tech/apps/crystalcraft ), which provides more possibilities for experimental scientists to consider element replacement and template structures based on crystal symmetry in terms of structure retrieval and generation.
