---
title: 纳米孔阵列
description: 入射光可与金属纳米结构表面电子相互作用形成表面等离激元共振(Surface Plasmon Resonance,SPR)，SPR具有突破衍射极限和局域场增强等独特的光学特性。本案例通过构建空气孔阵列金属薄膜结构模型，使用FDTD计算薄膜的透射和反射光谱，分析薄膜表面的近场分布和SPR引起的局域场增强。
language: zh-CN
businessId: nanohole-array
keywords: 时域有限差分(FDTD),纳米孔阵列,表面等离激元共振
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/nanohole_array_structures_20240119145000A051.jpg
---

# 前言

入射光可与金属纳米结构表面电子相互作用形成表面等离激元共振(SPR)，SPR 具有突破衍射极限和局域场增强等独特的光学特性。本案例通过构建空气孔阵列金属薄膜结构模型，使用 FDTD 计算薄膜的透射和反射光谱，分析薄膜表面的近场分布和 SPR 引起的局域场增强。

![structures](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_structures.png)

# 仿真设置

本案例使用 3D FDTD 进行仿真，构建周期孔阵列金属薄膜结构，结构如下图所示。本例中，金属薄膜的厚度为 100 nm，材料为金；圆柱空气孔的半径为 100 nm，周期间距为 400 nm；入射平面光的波段选为 400~750 nm。特别的是，当周期结构的周期单元为平面对称结构时，可将仿真区域对应轴向的最小和最大边界条件均设置为对称或反对称，等价于周期边界条件。在本案例中，周期单元和光源均为对称结构，在此使用对称/反对称边界条件代替周期边界条件（Periodic）以减小运算量，提高仿真效率。FDTD 仿真区域整体采用自动非均匀网格，在纳米孔结构处使用覆盖网格，提升网格精细度，尺寸为 10 nm，以获得更精准的仿真结果。

![structures](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_simulation_structures.png)

金属薄膜材料金的折射率样本参考自`CRC化学与物理手册`。根据材料数据拟合仿真模型，如下图所示，由图可以看出对应波段的折射率变化趋势。根据材料色散关系，可大致预测材料在 FDTD 仿真波段内的特性。

![material](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_Au_material_fit_1.png)

# 仿真结果

打开附件工程，运行仿真之后运行脚本文件可得到所有目标数据。
下图为`FDFP Monitor` `R`和`T`分别记录的反射和透射光谱，通过脚本文件计算可求得 R+T 光谱。从图中可以明显看出，大约在 675 nm 处有较强的共振现象。

![R+T](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_T_and_R_1.png)

如下图所示，将透射光谱归一化为空气孔的面积除以周期单元格的面积，可以看出部分波段的透射明显高于正常水平。

![cw_T](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_T_normalized_1.png)

下图为金薄膜透射与反射两边表面的$|E|^2$分布图。虽然入射场强度仅为 1$V/m$，但是对比透射/反射分布图的强度，可以明显看出局域近场的增强非常显著。

![abs(E)2_T](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_Transmitted_surface_E_1.png)
![abs(E)2_R](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_reflected_surface_E_1.png)

如下为 x=0 时 z-y 平面截面的场分布图。通过调整数据 colorbar 范围，可以清楚观察到哪些区域的近场强度被增强到 10 倍以上。

![abs(E)2](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_zyplane_surface_E_1.png)
