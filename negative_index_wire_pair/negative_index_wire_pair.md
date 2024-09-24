---
title: 短线对结构的负折射率材料
description: 负折射率超材料（Negative index metamaterial,NIM）是一种人造光学结构，它的折射率对于一定频率范围内的电磁波是负值。本文以J.Zhou论文中超材料结构进行仿真说明。
language: zh-CN
businessId: negative-index-metamaterial-using-wire-pairs
keywords: 时域有限差分(FDTD),负折射率超材料,等离子体
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/Negative_index_metamaterial_structure_20240119145619A052.jpg
---

# 前言

负折射率超材料（NIM）是一种人造光学结构，它的折射率对于一定频率范围内的电磁波是负值。本文以 J.Zhou 论文中超材料结构进行仿真说明。文献中使用多对铜线对，并由厚度为$ts$的电介质隔开，其单个周期结构如下图所示。

![negative_metamaterial_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Negative_index_metamaterial_structure.png)

# 仿真设置

在本案例中，使用 3D FDTD 仿真。依据文献当中的参数构建短线对结构如下图所示。其中光源采用 12~16GHz 频率的平面光源，来研究该结构的透射反射率。其中介质层的厚度$ts$为 254$\mu m$，相对介电常数为 2.53；在介质层上下两面都有 10um 厚的铜线对结构。因为铜在 12−16GHz 的频率下，介电常数的虚部非常大，以至于铜近似完美导电体，故在本案例中，我们使用 PEC（完美导电体）来代替金属铜。同时由于 10um 厚的铜在 z 方向上需要非常小的网格尺寸，因此仿真会需要较大的内存和较长的时间。为了降低仿真内存和时间，并且保持仿真结果的精度，我们可以使用 2D Structure 来代替三维结构。

![simulation_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Negative_index_simulation_structure.png)

由于仿真结构是对称周期结构，因此我们可以在两个边界上使用对称/反对称边界的组合，这样可以使仿真空间减少 3/4，进一步减少了仿真时间。此案例中，将“X axis min”和“X axis max”设置为“Symmetric”，将“Y axis min”和“Y axis max”设置为“Anti-Symmetric”。

# 仿真结果

仿真结束后，运行附件中的`negative_index_wire_pair.msf`脚本即得到该结构的传输和反射。该结果和文献上[^1]的仿真结果相似。

![transmission](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Negative_index_transmission.png)
![reflection](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Negative_index_reflection.png)

# 参考文献

[^1]: Zhou J , Zhang L , Tuttle G , et al. "Negative index materials using simple short wire pairs." Physical Review B, 73(4):041101.(2006)
