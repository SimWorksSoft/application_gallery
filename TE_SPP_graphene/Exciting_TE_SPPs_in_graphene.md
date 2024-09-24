---
title: 在石墨烯中激发表面等离子体
description: 石墨烯的化学势可以通过施加电压或者化学掺杂等方式进行调节，这使其得在物质与光相互作用领域有着极大的应用范围，尤其是表面等离子体（surface plasmon polaritons, SPPs）。石墨烯材料通过激发表面等离子体的方式，将大大增强其与光相互作用的能力。
language: zh-CN
businessId: exciting-the-surface-plasmon-polaritons-in-graphene
keywords: 时域有限差分(FDTD),石墨烯,光子晶体,等离子体
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/surface_plasmon_in_graphene_structures_20240119152811A055.jpg
---

# 前言

石墨烯材料从发现至今，因其优异的电学、热学、力学性能，引起了科学研究者的广泛关注。石墨烯的化学势可以通过施加电压或者化学掺杂等方式进行调节，这使其得在物质与光相互作用领域有着极大的应用范围，尤其是表面等离子体（surface plasmon polaritons, SPPs）。表面等离子体是一种电磁表面波，其场的能量大部分集中在金属表面，而在垂直界面方向上呈指数衰减。石墨烯材料通过激发表面等离子体的方式，将大大增强其与光相互作用的能力。
本案例将根据文献[^1]当中的工作，来研究石墨烯在满足表面等离子体共振条件时，石墨烯与光相互作用增强的现象。

# 仿真设置

本案例采用 2D FDTD 进行仿真，根据文献中所述，构建如下图所示结构。五层的光子晶体（Photonic Crystal）结构放置在玻璃衬底上，石墨烯薄膜放置在 PC 的表面，最外层覆盖一层 PMMA 材料。由于结构在 x，y 方向上均匀且无限延伸，为节省计算时间，在本案例中 x 方向上厚度仅取 10nm。同时光源使用平面波，其入射角度将在后续进行扫描。由于平面光源存在入射角，x 方向上需要使用`bloch`周期边界以模拟光源的斜入射。具体细节请参考[bloch 边界条件](/localhost/knowledge-base/User-Manual_boundary-condition-settings)。

![structures](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/surface_plasmon_in_graphene_structures.png)

## 材料

在 1.31$\mu m$的波段下，该结构中基底材料$SiO_2$的相对折射率为 1.4468，PC 结构由相对折射率为 2.7204 的$TiO_2$和相对折射率为 1.4468 的$SiO_2$交替组成，最上层的材料是相对折射率为 1.481 的 PMMA，背景材料为相对折射率为 1 的空气。石墨烯材料的散射率设置为 0.11meV、化学能为设置为 0.05eV，其拟合曲线如下所示，其余参数及细节请参考[石墨烯材料](/localhost/knowledge-base/User-Manual_graphene-material)。

![graphene_fit](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/surface_plasmon_in_graphene_material_fit.png)

# 仿真结果

打开附件工程并运行参数扫描，工程运行结束后再运行脚本文件`Exciting_TE_SPPs_in_graphene.msf`，参数扫描将对平面波入射角度进行扫描，扫描范围为 43 度到 51 度，其中透射率和反射率得到的结果如下所示，其中反射率趋势与参考文献当中的图二一致。可以看出入射平面波在符合表面等离子体共振波矢的角度时，石墨烯将产生表面等离子体共振，使得其对入射光的吸收得到极大的增强，此时几乎没有透射和反射。

![T_and_R](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/surface_plasmon_in_graphene_T_R_new.png)

该脚本还绘出了 z 方向上电场随入射角度变化的图像，如下图所示。结果表明，在 50.5 度时，电场在石墨烯层发生耦合，石墨烯所在的位置电场得到了增强。

![E2](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/surface_plasmon_in_graphene_E2_new.png)

# 参考文献

[^1]: I. Degli-Eredi, J. E. Sipe, and N. Vermeulen, “TE-polarized graphene modes sustained by photonic crystal structures”, Opt. Lett. Vol. 40, No. 9, pp. 2076-2079 (2015).
