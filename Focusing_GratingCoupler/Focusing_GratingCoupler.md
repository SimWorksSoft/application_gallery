---
title: 聚焦光栅
description: 硅光集成的一个重要问题是集成波导器件与光纤或自由空间光学器件之间的接口问题，光栅耦合器凭借其易制作、灵活度高、对准容差大等优点，成为解决芯片与光纤之间耦合难题的最主要的解决方案。本案例建模仿真了一个聚焦光栅，并研究了它的耦合损耗。
language: zh-CN
businessId: focusing-grating-coupler
keywords: 时域有限差分(FDTD),聚焦光栅耦合器，参数分析
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/focusingGratingCoupler_E146_20240304132515A020.jpg
---

# 前言

在许多数据通讯领域，高速光互连技术是进行大量数据交换的必要条件，因此光互连集成是近年来的热门研究课题。硅光集成技术以其优越的性能、低廉的成本以及易与其他光电元件单片集成等特点成为光互连集成最主要的候选技术。硅光集成的一个重要问题是集成波导器件与光纤或自由空间光学器件之间的接口问题，光栅耦合器凭借其易制作、灵活度高、对准容差大等优点，成为解决芯片与光纤之间耦合难题的最主要的解决方案。本案例根据$Hoffmann$等人的工作[^1]，建模仿真了一个聚焦光栅，研究了该聚焦光栅的耦合损耗。
![focusingGratingCoupler_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/focusingGratingCoupler_structure.png)

# 仿真设置

## 模型简介

本案例中使用的聚焦光栅耦合器是基于浅刻蚀$SOI$技术，其波导层为$Si$，上下包层都为$SiO_{2}$，衬底材料还是$Si$，如上图所示。$Z$方向为光波导传输方向，光波导厚度方向为$Y$方向。由于结构在$X$方向上对称，光源在$X$方向上反对称，因此我们在$X_{min}$方向上使用`Anti-Symmetric`反对称边界条件。

耦合光栅部分使用了共焦光栅，其工艺参数（波导厚度、埋氧层厚度、衬底厚度、包层厚度、浅蚀深度）使用 IME 规定的参数，光栅周期、占空比和 taper 的设计参考了文献[^1]。如下图所示，光栅本身将光聚焦到宽度$dwg=0.5\mu m$的硅线波导中，其中 taper 的张角为$\alpha=31.5^{\circ}$，$r$为$19.5\mu m$，在设计中，光栅图案为同心圆线，圆心位于与波导相交的楔形物的顶点。
![focusingGratingCoupler_gratingstructure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/focusingGratingCoupler_gratingstructure.png)

| Variables | Period/$\mu m$ | Duty |
| :-------: | :------------: | :--: |
|   Value   |      0.67      | 0.53 |

## 光源设置

阶跃型单模光纤出射的光被斜入射到光栅上，可以近似认为是`Gaussian`高斯光源的场分布，因此在本软件中可以使用高斯光源，只需使高斯光源的束腰尺寸与光纤的纤芯匹配，并且保证高斯光源位于纤芯的材料中即可。高斯光源无需进行解模，因此省略光纤元件模型，仅在光栅结构上方放置高斯光源即可。

# 仿真结果

下图显示了放置在聚焦光栅耦合器中的`FDFP`监视器中得到的波长为$1.46\mu m$时的电场分布图，可以看到高斯光源的光入射到光栅区域后，被光栅耦合到右侧的硅线波导中。
![focusingGratingCoupler_E146](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/focusingGratingCoupler_Efield.png)

下图为高斯光源距离硅线波导 $d=23\mu m$处时，硅线波导中的`FDFP`监视器得到的透射率随波长的分布图，从图中可以看出，该聚焦光栅耦合器在波长为$1.56\mu m$处能够达到最大的透射率，为$52\%$。
![focusingGratingCoupler_T](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/focusingGratingCoupler_T.png)

# 参数分析

附件中的工程包含一个设置好的参数化扫描，可以对光源距离硅线波导从$23\mu m$到$25\mu m$之间的范围进行扫描。扫描结束后可以得到透射率 T 随光源位置变化的分布图，如下图。从图中可以看出，当光源距离硅线波导$24.33\mu m$时，该聚焦光栅耦合器可以在波长为$1.556\mu m$处达到最大的透射率，为$51.97\%$。
![focusingGratingCoupler_sweep](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/focusingGratingCoupler_sweep.png)

# 参考文献

[^1]: Hoffmann J ,Schulz M K ,Pitruzzello G , et al.Backscattering design for a focusing grating coupler with fully etched slots for transverse magnetic modes[J].Scientific Reports,2018,8(1):1-8.
