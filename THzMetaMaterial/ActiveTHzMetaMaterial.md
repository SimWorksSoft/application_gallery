---
title: 太赫兹超材料
description: 超材料是一种具有特殊性质的人造材料。这种材料可以调控电磁波的频率、幅度、相位和极化等基本的物理特征。本案例对Chen等人的论文中的无源超材料进行仿真，分析该超材料的表面电流密度。
language: zh-CN
businessId: thz-metamaterial
keywords: 时域有限差分(FDTD),太赫兹超材料,表面电流密度
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/Active_THz_Metamaterial_structure_20240117165143A048.jpg
---

# 前言

“超材料（Metamaterial）”是一种自然界没有的，具有特殊性质的人造材料。这种材料可以调控电磁波的频率、幅度、相位和极化等基本的物理特征。太赫兹超材料是针对频率在太赫兹范围内的电磁波进行调控的超材料。本案例对*Chen*等人的论文*Active teraherz metamaterial devices[^1]* 中的无源超材料进行仿真，分析该超材料的表面电流密度。

# 仿真设置

## 结构简介

本案例中使用的太赫兹超材料由砷化镓（GaAs）基底以及其表面的金（Au）层组成，其结构如下图所示。参考文献中使用的金的厚度为$0.2 \mu m$，远小于仿真中使用的波长（130$\mu m$ - 1200$\mu m$），因此在本案例中可以使用`2D Structure`来构建金层。由于仿真结构及光源在 X 方向上是对称的，我们在$X_{min}$和$X_{max}$方向上使用`Symmetric`对称边界条件。

![Active_THz_Metamaterial_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Active_THz_Metamaterial_structure.png)
|参数|A|D|G|W|
|:-----:|:-----:|:-----:|:-----:|:-----:|
|值（$\mu m$）|36|10|2|4|

## 材料设置

使用 Drude 模型（其中包含等离子体频率$\omega_p$和碰撞频率$\gamma_p$）来表示金材料。在低频极限（$\omega_p << \gamma_p$）时，Drude 模型可以表示为一个简单的导电模型，因此本案例使用`Perfect electric condutor(PEC)`完美电导体材料来代替金材料。

# 仿真结果

## 反射率与透射率

根据器件顶部与底部的`Frequency-Domain Field and Power(FDFP)`频域场功率监视器得到的 T 数据，绘制出该结构的反射率（R）和透射率（T）随频率的函数图如下，可以看到该超材料器件的共振频率约为 0.66THz 和 1.7THz，与参考文献**Figure3a**的结果吻合。

![Active_THz_Metamaterial_RT](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Active_THz_Metamaterial_RT.png)

## 电场分布及表面电流密度

下图为使用附件中的脚本文件绘制出的在共振频率为 0.66THz 时，超材料器件表面的电场分布以及表面电流密度分布图。从图中可以看出，在谐振频率 0.66THz 下，电场高度集中于分裂间隙处，超表面单元之间连接的金属线上没有明显的表面电流。

![Active_THz_Metamaterial_E](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Active_THz_Metamaterial_E.png)![Active_THz_Metamaterial_K](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Active_THz_Metamaterial_K.png)

# 参考文献

[^1]: H.-T. Chen et al., "Active terahertz metamaterial devices", Nature 444, 597-600 (2006)
