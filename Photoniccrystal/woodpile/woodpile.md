---
title: 木堆晶格能带结构
description: 木堆晶格（woodpile Lattice）光子晶体一般由一堆交替垂直排列的长方体介质组成。本案例结合现有文献，构建木堆晶格光子晶体模型，使用FDTD求解器探究此光子晶体的能带结构。
language: zh-CN
businessId: bandstructure-of-woodpile-lattice
keywords: 能带结构,木堆晶格,光子晶体,时域有限差分(FDTD)
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/woodpile_lattice_20240305092330A029.jpg
---

# 前言

木堆晶格（woodpile Lattice）光子晶体一般由一堆交替垂直排列的长方体介质组成。本案例结合现有文献[^1]，构建木堆晶格光子晶体模型，使用 FDTD 求解器探究此光子晶体的能带结构。

![woodpile_lattice.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/woodpile_lattice.png)

# 仿真设置

## 模型简介

本案例使用 FDTD 求解器分析由均匀介质棱柱按木堆晶格结构周期排列组成的光子晶体的能带结构。无限长的介质棱柱在空气中平行排列并垂直交叉堆积实现了空间中周期性变化的折射率分布，形成光子带隙[^2]。对于本模型，由折射率为 3.47851 的介质棱柱组成的木堆晶格光子晶体拥有完全禁带。有关本案例中木堆结构、木堆晶格布里渊区及特殊点坐标的详细信息，请见参考文献[^1]。

## 模型构建

本案例的模型构建和仿真设置与案例[2D 正方晶格能带结构](/localhost/case-detail/bandstructure-of-2d-square-lattice)相似。附件 woodpile.mpps 为本案例的展示文件，打开文件可以查看详细的模型参数及设置。本软件内置结构组库中拥有 woodpile 结构模型，用户可以直接选择并进行插入。为了满足周期性边界条件，在 FDTD 的仿真区域中必须包含两个周期性结构单元。因此，需要在两个晶格结构单元内构建相匹配的偶极子源，以避免人为区域折叠的问题。相似的问题请见[三角晶格光子晶体](/localhost/case-detail/bandstructure-of-2d-triangular-lattice)。

## 仿真结果

下载并打开附件 woodpile.mpps，运行所有的参数扫描。运行完成所有的参数扫描后，下载并运行脚本文件 woodpile.msf，以获取扫描结果并绘制能带结构图，如下图所示。

![woodpile_band.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/woodpile_band.png)

# 参考文献

[^1]: "Photonic Crystal Laser-Driven Accelerator Structures", A dissertation submitted to the department of physics and the committee on graduate studies of Stanford University in partial fulfillment of the requirements for the degree of Doctor of Philosophy, Benjamin Cowan, March 2007 - Chapter 3.
[^2]: Ho K M , Chan C T , Soukoulis C M , et al. Photonic band gaps in three dimensions: New layer-by-layer periodic structures[J]. Solid State Communications, 1994, 89( 5):413-416.
