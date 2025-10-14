---
title: 使用三阶非线性材料进行四波混频
description: 在非线性光学中，四波混频（Four-Wave Mixing, FWM）是一种典型的三阶非线性效应，被广泛应用于全光信号处理、波长转换和新光源产生等领域。当光在具有 Kerr 非线性的材料中传播时，多频率光场通过非线性相互作用会激发出新的频率分量，实现频率混合与能量转移。本案例展示了一个基于三阶非线性材料的 FDTD 四波混频仿真流程。
language: zh-CN
businessId: four-wave-mixing-with-nonlinear-material
keywords: 时域有限差分(FDTD),非线性光学,克尔效应,四波混频
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/fourwave_cover.jpg
---

# 前言
在非线性光学中，四波混频（Four-Wave Mixing, FWM）是一种典型的三阶非线性效应，被广泛应用于全光信号处理、波长转换和新光源产生等领域。当光在具有 Kerr 非线性的材料中传播时，多频率光场通过非线性相互作用会激发出新的频率分量，实现频率混合与能量转移。时域有限差分法（Finite-Difference Time-Domain, FDTD）能够在时域直接求解包含非线性项的麦克斯韦方程，完整捕捉电场在非线性介质中的演化过程，因此是研究四波混频的有效工具。本案例展示了一个基于三阶非线性材料的 FDTD 四波混频仿真流程。

# 仿真设置
## 模型简介
本案例中关于非线性仿真的特殊仿真设置（如 `override bandwidth for mesh generation`、 光源强度、光源脉冲，归一化等），与案例[使用非线性材料产生谐波](/localhost/case-detail/harmonic-generation-with-nonlinear-materials)相似，在此不再展开介绍。详细模型可以通过附件中的 *four_wave.mpps* 工程文件查看。本案例中设置了三个平面波光源，频率分别为 $100\ THz, 120\ THz$和 $140\ THz$，并同时入射到非线性平板。您可以通过禁用部分光源来观察单个光源或多光源作用下的仿真结果。

![fourwave_simulation](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/fourwave_simulation.png)

## 材料设置
本案例使用的材料为三阶非线性材料，其基底材料设置为二氧化硅。对于二氧化硅光纤，典型参数如下图所示：其中 $chi1 \ chi2\ chi3$ 分别为一阶、二阶、三阶非线性极化系数； $alpha$ 表示克尔效应在总非线性效应（克尔+拉曼散射）中的占比， $omega \space raman$ 为非线性拉曼角频率， $delta \space raman$ 为共振线宽。

![fourwave_material](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/fourwave_material.png)

# 仿真结果
## 单光源激发
当仅启用一个光源时，光场通过非线性平板会激发三次谐波成分。如下图所示，分别为 $100\ THz$、 $120\ THz$ 和 $140\ THz$入射时的输出频谱：

![fourwave_100THz](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/fourwave_f_100THz.png)

![fourwave_120THz](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/fourwave_f_120THz.png)

![fourwave_140THz](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/fourwave_f_140THz.png)

## 四波混频
当三个光源同时入射时，不同频率之间的相互作用会激发出新的频率分量，在输出频谱中表现为一系列额外的波峰，这正是四波混频效应的结果：

![fourwave_mix](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/fourwave_mix.png)