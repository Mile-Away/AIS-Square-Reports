# 2024 Q2 OpenLAM Report｜更稳定的代码 更丰富的领域模型 

## 代码
- DeePMDkit-v3-beta版本 (v3.0.0b3) 发布。相较于早前发布的alpha版本，beta版本对代码进行了更完整的重构，对各个模型模块有了更全面的支持，优化了DPA2模型对LAMMPS的支持，也添加了更多新功能。v3.0.0b3版本进一步修复了v3.0.0b0，v3.0.0b1和 v3.0.0b2中的已知bug，也通过了系统性测试，并且也发布了适用于v3.0.0b3 的DPA2预训练模型 (见下文) 。详细的功能支持和优化可见release note：
  - https://github.com/deepmodeling/deepmd-kit/releases/tag/v3.0.0b0
  - https://github.com/deepmodeling/deepmd-kit/releases/tag/v3.0.0b1
  - https://github.com/deepmodeling/deepmd-kit/releases/tag/v3.0.0b2 
  - https://github.com/deepmodeling/deepmd-kit/releases/tag/v3.0.0b3 (推荐使用)
- ABACUS软件发布v3.7版本更新。ABACUS新版本针对合金领域进行了全面测试，确保了计算准确性和赝势可靠性。同时，为了支持OpenLAM大原子模型计划，进行了深入优化，提升了在国产DCU硬件上的性能，包括内存使用效率和计算速度，进一步扩展了其在大原子模型第一性原理标签计算中的应用范围。详情请参见https://mp.weixin.qq.com/s/oAFKJzhjV1eghaYTqiWUbQ

## 数据
- 高压富氢化合物数据
  - 包含14万数据，29种元素的三元富氢化合物，覆盖压力范围为150 - 250 GPa 的高压富氢化合物数据库。数据链接：https://www.aissquare.com/datasets/detail?pageType=datasets&name=High-Pressure-Hydrogen-Rich-Compound&id=257
- 固态电解质数据 (SSE-ABACUS) 
  - 包含12.7万数据，27种元素, 365个体系(包含硫化物，卤化物，掺杂和界面)。数据链接：https://www.aissquare.com/datasets/detail?pageType=datasets&name=SSE-abacus&id=260
## 模型
- 基于DeepMDkit-v3-beta版本的预训练模型
  - 更新了与DeePMD-kit-beta版本 (v3.0.0b3) 适配的多任务DPA-2预训练模型 https://www.aissquare.com/models/detail?pageType=models&name=DPA-2.2.0-beta3&id=272
  - 和DPA-2单任务预训练模型 

数据集        | Dataset card | Model card
------------|--------------|------------
SSE-ABACUS  | https://www.aissquare.com/datasets/detail?name=SSE-abacus&id=260&pageType=datasets | https://www.aissquare.com/models/detail?pageType=models&name=SSE-ABACUS-dpa2&id=267
SSE-VASP    | https://www.aissquare.com/datasets/detail?name=Solid_State_Electrolyte&id=217&pageType=datasets | https://www.aissquare.com/models/detail?pageType=models&name=SSE-VASP-dpa2&id=266
电解液      | https://www.aissquare.com/datasets/detail?name=Electrolyte&id=216&pageType=datasets | https://www.aissquare.com/models/detail?pageType=models&name=Electrolyte-dpa2&id=268

- 领域模型
  - Free Energy Pertubation Model  (https://arxiv.org/pdf/2406.09817) 
    - NNP上，使用DPA-2 + semi-empirical method达到与DFT相当的精度
    - 设计了新的NNP调优分子力场流程，同时保证了NNP级别的势能面准确度和MM级别的计算效率
  - 固态电池
    - 构建了固态电解质预训练大模型DPA-SSE(SSE-ABACUS数据集)。模型预测的能量精度相比于CHGNET和M3GNET力场高出1个数量级，受力精度提升1~5倍。在动力学性质上，DPA-SSE预测的Li离子的扩散系数和电导率，和实验具有良好的一致性。
    - 块体材料(硫族化合物)的预训练模型,上线至arXiv (http://arxiv.org/abs/2406.18263)
    - 开发固态电解质预训练模型的专用app (https://bohrium.dp.tech/apps/voltcraft) 
  - 合金
    - 构建了包含53种元素的合金预训练大原子模型，采用国产abacus软件和DCU机器进行第一性原理计算，共产生2.4万数据。构型包括单质、化合物、高熵合金晶体结构，空位、自间隙、表面等缺陷结构，压强范围为-0.5-5 GPa，温度范围为50-3000 K。训练后模型能量精度可小于35 meV/atom，力精度可小于0.25 eV/Å。
    - 与已有MACE预训练大原子模型相比，开发出的合金领域模型在弹性常数、模量、表面能、点缺陷形成能等性质方面均表现更好。
  - 高压富氢化合物
    - 构建了适用于高压富氢超导化合物结构预测的原子尺度模型 (包含152702数据集，29种元素的三元富氢化合物，覆盖压力范围为150 - 250 GPa) 。
    - 该DPA-1模型基于2024Q1版本，目前能够稳定优化28种已知富氢超导化合物的结构，优化前后空间群保持一致。 (https://www.aissquare.com/models/detail?pageType=models&name=High-Pressure-Hydrogen-Rich-Compound&id=258) 
  - 动态催化
    - 初步构建了团簇表面动态催化基元反应的通用势函数模型DPA-DynaCat，其训练集包括 Au/Ag/Cu/Pt/Pd/Ni纯金属及二元合金团簇表面发生的H2/O2/H2O/CO/CO2/CH4等常见小分子相关基元反应。
    - 模型相比于DFT计算的结果可以给出势能面的准确预测，同时相比于针对单一体系的机器学习势函数可以得到近似的反应自由能。通过此模型可以结合分子动力学进行增强采样，考虑反应过程中各异构体所带来的贡献，进而可用于计算反应能垒和反应自由能。 (https://www.aissquare.com/models/detail?pageType=models&name=DPA-DynaCat&id=262) 

## 社区
- 《全元素周期表晶体结构集邮大赛》于7月1日正式开赛。这将是一个长期有效的比赛，旨在为晶体结构搜索生成算法提供测试、迭代的平台，同时为OpenLAM的更新提供更丰富的化学空间。详情请参见 (https://bohrium.dp.tech/competitions/8821838186?tab=introduce) 
- 基于晶体结构集邮大赛，构建了OPENLAM晶体结构数据库，目前已收录五十余万稳定结构。数据库中所有结构均可通过官方API进行访问 (https://github.com/deepmodeling/openlam) ；为了促进实验科学家的语言和视角与当前的人工智能技术和数据库进展的有效连接，我们开发了Crystal Craft APP (https://bohrium.dp.tech/apps/crystalcraft) ，在结构检索、生成方面，为实验科学家在基于晶体对称性考虑元素替换、模板结构提供更多可能性。
- 
