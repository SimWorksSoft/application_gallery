---
title: 具有光子晶体结构的有机太阳能电池
description: 如何提高太阳能电池的转换效率，是目前亟待解决的问题。较常用的一种方法是在有机太阳能电池光活性层（OSCs）中增加微纳米陷光结构来提高光吸收，从而达到提高转换效率的目的。其中在OSCs的光活性层使用光子晶体结构，可以增强太阳能电池对特定波段的光吸收。本案例使用FDTD仿真分析具有2D六角晶格光子晶体结构的有机太阳能电池的光吸收。
language: zh-CN
businessId: organic-solar-cell-with-pc-structure
keywords: 时域有限差分(FDTD),有机太阳能电池,光子晶体(PC),光吸收,光电转换效率(PCE)
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/solar_organic_structure_20240117163819A047.jpg
---

# 前言

有机太阳能电池（Organic solar cells, OSCs）由于人们对清洁能源的需求和重量轻、机械柔性、制造成本低等优点，逐渐成为太阳能电池领域的研究热点[^1]。如何提高其转换效率，是目前亟待解决的问题。较常用的一种方法是在 OSCs 光活性层中增加微纳米陷光结构来提高光吸收，从而达到提高转换效率的目的。其中在 OSCs 的光活性层使用光子晶体结构，可以增强太阳能电池对特定波段的光吸收。本案例使用 FDTD 仿真分析具有 2D 六角晶格光子晶体结构的有机太阳能电池的光吸收。

![solar_organic_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_structure.png)

# 仿真设置

本案例使用的有机太阳能电池中，光活性层为*聚-3-己基噻吩/[6,6]-苯基-C61-丁酸甲酯（P3HT:PCBM）[^2][^3]* 的本体异质结混合物。本体异质结的内部含有由氧化锌纳米晶形成的光子晶体结构，利用入射太阳光与光子晶体波导的漏模共振，可以提高太阳能电池对部分波段的光吸收[^4]。

太阳能电池的结构和材料决定着转换效率，本案例中的有机太阳能电池为内部含有光子晶体纳米结构的多层电池结构模型。对于本模型中光子晶体的材料氧化锌的折射率为 1.40，周期性排列的氧化锌圆柱的半径 r 为 0.15 μm，高度为 0.12 μm，构成六角晶格的晶格间距 a 为 0.46 μm，氧化锌基底的厚度为 0.07 μm。氧化锌光子晶体基底上为体异质结光活性层，厚度为 0.193 μm。结构再往上为一层导电聚合物水溶液 PEDOT:PSS，厚度为 0.05 μm。电池表面为厚度为 0.178 μm 的导电玻璃（ITO），最上层由玻璃覆盖，玻璃的折射率为 1.52。

本案例器件构建方式与硅基太阳能电池案例（[介绍](/localhost/case-detail/planar-silicon-solar-cell)）相似，在此不再重复，请下载附件 *OrganicSolarCellwithPC.mpps* 查看详细信息。电池结构中的光子晶体为 2D 六角晶格结构，请参考 2D 六角晶格能带结构案例说明文档（[2D 六角晶格能带结构](/localhost/case-detail/bandstructure-of-2d-triangular-lattice)）获取更多相关信息。

## 材料设置

为了在仿真中建立 P3HT:PCBM、ITO、PEDOT:PSS 和铝的材料模型，我们需要在软件中添加新的 3D 采样数据模型并导入附件中对应材料的采样数据.txt 文件。下图中显示了在 400nm 到 700nm 的太阳光谱范围内，四种材料的拟合曲线。这些材料数据摘自文献[^5][^6][^7]。

![solar_organic_PSS_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_PSS_fitting.png)![solar_organic_PCBM_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_PCBM_fitting.png)

![solar_organic_ITO_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_ITO_fitting.png)![solar_organic_Al_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_Al_fitting.png)

# 仿真结果

通过光活性层顶部和底部的`FDFP`监视器中的 T 数据，可以绘制出光活性层的光吸收光谱图如下。可以看出光活性层在太阳光谱范围内尤其是 400nm-600nm 部分具有较高的吸收率。

![solar_organic_Absorption](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_Absorption.png)

将附件中工程的六角晶格光子晶体结构组禁用后重新仿真可以得到无光子晶体结构的有机太阳能电池光活性层的吸收情况，绘制出在有和没有光子晶体时光活性层的吸收曲线如下图：

![solar_organic_Absorption_without_PC](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_Absorption_without_PC.png)

如上图所示，在有光子晶体时有机太阳能电池的吸收率较无光子晶体结构，在 673nm 左右略有增强。这种增强是由于光子晶体本身的光子带隙造成的，可由能带结构分析组来进一步探究其能带结构。

# 参考文献

[^1]: Shi T , Zhang Z , Guo X , et al. Ultrafast Charge Generation Enhancement in Nanoscale Polymer Solar Cells with DIO Additive[J]. Nanomaterials, 2020, 10(11):2174.
[^2]: Tumbleston J R , Ko D H , Samulski E T , et al. Electrophotonic enhancement of bulk heterojunction organic solar cells through photonic crystal photoactive layer[J]. Applied Physics Letters, 2009, 94(3):25.
[^3]: Tumbleston J R , Ko D H , Samulski E T , et al. Absorption and quasiguided mode analysis of organic solar cells with photonic crystal photoactive layers[J]. Optics Express, 2009, 17(9):7670-7681.
[^4]: Ko D H , Tumbleston J R , Zhang L , et al. Photonic Crystal Geometry for Organic Solar Cells[J]. Nano Letters, 2009, 9(7):2742.
[^5]: Monestier F , Simon J J , Torchio P , et al. Modeling the short-circuit current density of polymer solar cells based on P3HT:PCBM blend[J]. Solar Energy Materials & Solar Cells, 2007, 91(5):405-410.
[^6]: Tumbleston J R , Ko D H , Lopez R , et al. Characterizing enhanced performance of nanopatterned bulk heterojunction organic photovoltaics[J]. International Society for Optics and Photonics, 2008.
[^7]: Palik, E. D. Handbook of optical constants of solids[M]. Academic press, 1998.
