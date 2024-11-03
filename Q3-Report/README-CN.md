# 2024 Q3 OpenLAM Report｜更准更快预训练模型发布，晶体结构比赛火热进行中

## 代码
DeePMD-kit V3.0.0 beta4版本发布，新功能和优化：
- __DPA2 整体优化__:
    -   __模型结构优化__：包括引入三体编码信息、优化消息传递更新过程等，提升了模型训练精度；新增了`small`、`medium` 和 `large`三种模型配置，用户可以根据不同应用场景选择合适的模型（详情见 https://github.com/deepmodeling/deepmd-kit/tree/v3.0.0b4/examples/water/dpa2）。
    -   __精度和性能提升__： 相比 beta3 版的 DPA2 模型，beta4 版的 DPA2-medium 模型在从头训练的`能量精度上提升了约 30%`（受力提升约14%），`训练和推理效率提升了约 2 倍`。

        - `DPA2-b4-medium` vs. `DPA2-b3` __精度benchmark__（27个数据集从头训练的平均测试误差，训练`1M steps, batch_size: "auto:256"`）


        | Model              | Energy Weighted RMSE (meV/atom) | Force Weighted RMSE (meV/Å) |
        |--------------------|------------------------------------|------------------------------|
        | DPA2-b4-medium     | __13.1__                               | __113.1__                        |
        | DPA2-b3            | 18.5                               | 130.8                        |

          
          - 训练速度（以192 原子 water体系为例， 单卡40G A800）：
          
        | Model            | Training Speed (s/100 steps) |
        |------------------|------------------------------|
        | DPA2-b4-medium   | __8.4__                          |
        | DPA2-b3          | 15.9                         |
- __新增性质预测功能__：支持对各种包含性质的数据进行直接训练、预测，提升了模型的应用范围，详细案例见：https://github.com/deepmodeling/deepmd-kit/tree/v3.0.0b4/examples/property。
- __新增描述符__： three body type embedding  (se_t_tebd)，使用案例见 https://github.com/deepmodeling/deepmd-kit/tree/v3.0.0b4/examples/water/se_e3_tebd。
- __代码结构优化和稳定性提升__：修复了日常使用中的已知问题，提升了代码的稳定性和可维护性。

详细的发布说明见： https://github.com/deepmodeling/deepmd-kit/releases/tag/v3.0.0b4。

## 数据
- 新增 Materials Project Trajectory 数据集（MPtraj，deepmd mixed type 格式）：
数据集链接：https://www.aissquare.com/datasets/detail?pageType=datasets&name=MPtraj&id=278。

## 模型

- __预训练模型__：
    -  __新版本__：适配V3.0.0 beta4 代码的`DPA2 medium multi-task 预训练模型（2.3.0-b4-medium`，模型链接：https://www.aissquare.com/models/detail?pageType=models&name=DPA-2.3.0-v3.0.0b4&id=279。
    -  __性能提升__：相比 Q2 发布的预训练模型（2.2.0-b3），新模型加入了 MPtraj 数据集，__在保持模型精度的同时，推理速度提升2倍__：
      推理速度对比（以192 原子 water体系为例， 单卡40G A800）
    
        | Pretrained Model            | Python inference speed (s/100 times) |
        |------------------|------------------------------|
        | [2.3.0-b4-medium](https://www.aissquare.com/models/detail?pageType=models&name=DPA-2.3.0-v3.0.0b4&id=279)  | __3.7__                          |
        | [2.2.0-b3](https://www.aissquare.com/models/detail?pageType=models&name=DPA-2.2.0-v3.0.0b3&id=272)        | 6.3                       |
    -  适配 V3.0.0 beta4 代码的 DPA2 small 和 large 预训练模型将在后续发布。更多信息见AIS Square主页：https://www.aissquare.com/openlam。
- __其他领域模型更新__：
    -   合金领域模型：开发了针对大模型的property-driven fine-tuning工作流，可同时对多种性质进行fine-tune，为得到针对特定应用的势函数模型提供助力，相应的bohrium notebook在[Finetune Alloy Property using APEX + DPGen2 | Bohrium](https://bohrium.dp.tech/notebooks/38767882597)。DPA-1&2合金大模型已上传至[AISSquare](https://www.aissquare.com/models/detail?pageType=models&name=DPA-1%262-53-alloy-multitask-400w&id=280)。

## 社区

- OpenLAM 晶体集邮大赛已开展二十余期，在比赛中涌现出许多优秀的结构生成算法，其中更是有连续霸榜多期的[Con-CDVAE算法](https://bohrium.dp.tech/competitions/8821838186?tab=discuss&postId=8415617783)。为了鼓励算法的多样性，我们通过对选手提交数据的分析，有针对性的调整了[评价标准](https://bohrium.dp.tech/competitions/8821838186?tab=discuss&postId=4170270451)。 目前比赛数据库中已经积累了1300余万晶体结构，其中由参赛选手贡献的结构已超过500万。
- 上述数据库中的所有结构信息均已开源，我们提供了两种数据获取方式：
  - Python api （https://github.com/deepmodeling/openlam）：已放开所有结构和相关能量预测信息。
  - App （https://bohrium.dp.tech/apps/crystalcraft）：支持多种检索功能与结构分析。

- 在这里我们也邀请各位社区成员和我们一道，共同开发打磨这个数据库作为社区的公共设施，不管是用户反馈，功能需求，还是数据画像，我们都期待听到你的声音。