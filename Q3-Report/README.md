# 2024 Q3 OpenLAM Report｜Enhanced Precision and Efficiency with New Pre-trained Models, Ongoing Crystal Structure Competition

## Code
DeePMD-kit V3.0.0 beta4 version released, new features and optimizations:
- __DPA2 Overall Optimization__:
    -   __Model Architecture Optimization__：The introduction of three-body embedding and optimization of the message passing update enhances model training accuracy; Three new model configurations (`small`, `medium`, and `large`) are available,  allowing users to select the appropriate model based on different application scenarios.（For more details, refer to  https://github.com/deepmodeling/deepmd-kit/tree/v3.0.0b4/examples/water/dpa2）.
    -   __Accuracy & Performance Improvement__： Compared to the beta3 version, the beta4 version of the DPA2-medium model demonstrates `approximately a 30% improvement in energy accuracy` (with about a 14% increase in force accuracy) and a `twofold increase in training and inference efficiency`.

        - `DPA2-b4-medium` vs. `DPA2-b3` __accuracy benchmark__（average RMSE of 27 datasets trained from scratch, training `1M steps, batch_size: "auto:256"`）


        | Model              | Energy Weighted RMSE (meV/atom) | Force Weighted RMSE (meV/Å) |
        |--------------------|------------------------------------|------------------------------|
        | DPA2-b4-medium     | __13.1__                               | __113.1__                        |
        | DPA2-b3            | 18.5                               | 130.8                        |

          
          - Training speed (using a 192-atom water system as an example, on a single 40G A800 card)：
          
        | Model            | Training Speed (s/100 steps) |
        |------------------|------------------------------|
        | DPA2-b4-medium   | __8.4__                          |
        | DPA2-b3          | 15.9                         |
- __Property Prediction__：Added support for direct training and prediction of various datasets containing properties, expanding the model's application scope. For detailed examples, see：https://github.com/deepmodeling/deepmd-kit/tree/v3.0.0b4/examples/property.
- __New Descriptor__： Introduced a three-body type embedding descriptor (se_t_tebd).  For a use case, refer to https://github.com/deepmodeling/deepmd-kit/tree/v3.0.0b4/examples/water/se_e3_tebd.
- __Code Refactor & Stability Improvement__：Addressed known issues, enhancing the code's stability and maintainability.

Detailed release notes are available at: https://github.com/deepmodeling/deepmd-kit/releases/tag/v3.0.0b4.

## Data
- __New Dataset__: Materials Project Trajectory dataset (MPtraj, deepmd mixed type format):
Dataset link: https://www.aissquare.com/datasets/detail?pageType=datasets&name=MPtraj&id=278。

## Model

- __Pre-trained Model__:
    -  __New Version__：Compatible with V3.0.0 beta4 code of `DPA2 medium multi-task pre-trained model(2.3.0 -b4-medium)`. Model link: https://www.aissquare.com/models/detail?pageType=models&name=DPA-2.3.0-v3.0.0b4&id=279
    -  __Performance Improvement__ : The new model, compared to the previously released Q2 pre-trained model (2.2.0-b3), integrates the MPtraj dataset, achieving a `twofold increase in inference speed while maintaining model accuracy`:
    Comparison of inference speed (using a 192-atom water system, on a single 40G A800 card)

        
        | Pretrained Model            | Python inference speed (s/100 times) |
        |------------------|------------------------------|
        | [2.3.0-b4-medium](https://www.aissquare.com/models/detail?pageType=models&name=DPA-2.3.0-v3.0.0b4&id=279)  | __3.7__                          |
        | [2.2.0-b3](https://www.aissquare.com/models/detail?pageType=models&name=DPA-2.2.0-v3.0.0b3&id=272)        | 6.3                       |

    -  DPA2 small and large pre-trained models adapted to V3.0.0 Beta4 code will be released in the future. For more information, see the AIS-Square homepage: https://www.aissquare.com/openlam
- __Other Domain Model Updates__：
    -   __Alloy Domain Model__: we developed a property-driven fine-tuning workflow for large atomic models, which can fine-tune multiple properties at the same time, providing assistance for obtaining potential function models for specific applications. The corresponding bohrium notebook can be found at[Finetune Alloy Property using APEX + DPGen2 | Bohrium](https://bohrium.dp.tech/notebooks/38767882597)。The Alloy Domain Models (DPA1 & DPA2) have been uploaded to [AISSquare](https://www.aissquare.com/models/detail?pageType=models&name=DPA-1%262-53-alloy-multitask-400w&id=280).

## Comunity

- The OpenLAM Crystal Philately Competition has been held for over 20 sessions, producing numerous excellent structure generation algorithms, including the top-ranking [Con-CDVAE algorithm](https://bohrium.dp.tech/competitions/8821838186?tab=discuss&postId=8415617783)。To promote algorithm diversity, we have revised the [evaluation criteria](https://bohrium.dp.tech/competitions/8821838186?tab=discuss&postId=4170270451) based on submitted data analysis. The competition database now contains over 13 million crystal structures, with contestant contributions exceeding 5 million.
- All the structural information in the above database has been open-sourced. We provide two ways to obtain data:
  - Python api （https://github.com/deepmodeling/openlam）：All structure and related energy prediction information are available via this repo.
  - App （https://bohrium.dp.tech/apps/crystalcraft）：Supports multiple search functions and structural analysis.

- We invite all community members to contribute to the development and enhancement of this database. Your feedback, functional requirements, and data profiling insights are highly valued.