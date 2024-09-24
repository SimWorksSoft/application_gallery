---
title: 硅基双直波导微环谐振腔
description: 硅基双直波导微环谐振腔中特殊的微环结构使得满足其谐振条件的光波在微环内干涉叠加，产生谐振，具有波长选择的功能。因此微环谐振腔被广泛应用于多个领域。其中典型的双直波导光学环腔结构由两个平行的直波导以及波导之间的微环组成，结构模型如图所示。本文简要介绍使用FDTD求解器仿真微环谐振的操作流程及注意事项。
language: zh-CN
businessId: silicon-based-double-straight-waveguide-microring-resonator
keywords: 硅基双直波导微环谐振腔,时域有限差分(FDTD),Q分析,仿真控制平台,SOI
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/ring_fdfp_data_e2_20240304131909A018.jpg
---

# 前言

硅基双直波导微环谐振腔中特殊的微环结构使得满足其谐振条件的光波在微环内干涉叠加，产生谐振，具有波长选择的功能。因此微环谐振腔被广泛应用于多个领域。其中典型的双直波导光学环腔结构由两个平行的直波导以及波导之间的微环组成，结构模型如图所示。本文简要介绍使用 FDTD 求解器仿真微环谐振的操作流程及注意事项。

![orring3d.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/orring3d.png)

# 仿真设置

## 模型简介

双直波导微环谐振腔结构模型的主要参数有微环半径、波导间距、波导宽和波导高度。本模型采用波导横截面尺寸为$0.4 \mu m×0.22 \mu m$的 SOI 结构，其中双直波导宽度$wg_{width}$与微环波导宽度$ring_{width}$相等，波导间距$gap$为$0.1 \mu m$。如果光在微环波导中传播一圈改变的相位正好等于$2 \pi$的整数倍，即满足相干条件时，所有耦合进微环的光波相互干涉会产生谐振增强效应，如下公式所示。

$$2 \pi R n_{eff,wg} = m \lambda  $$

根据公式可求解满足谐振要求的微环半径$R$。当输入源中心波长为$1.55 \mu m$时，根据模式求解器对波导求解光模式的有效折射率，可求得当$m = 25$时，对于$0.4 \mu m×0.22 \mu m$的 SOI 结构，理论计算的微环半径$R$约为$2.9 \mu m$。

## 求解器设置

本次仿真使用 FDTD 求解器。FDTD 针对时域计算得到时间信号，使用傅里叶变换可以到频域的结果。对于微环谐振腔这种高 Q 器件，为了得到更准确的仿真结果，需要较长的仿真时间，本案例设置为 5 ps。为了提升仿真效率并保持计算精度，将网格类型设置为自动非均匀网格，精细程度为 4，网格细化方式选为 Conformal variant VP-EP。此外，为了保证端口精准的模式求解，在波导与环的耦合区域覆盖均匀细化网格。
注：本软件支持使用脚本构建和编辑仿真模型，更多内容见[脚本函数](/localhost/knowledge-base/Script-Commands_script-commands-overview)功能介绍。附件有构建器件和仿真设置的脚本文件。

![ring_vpep_mesh.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/ring_vpep_mesh.png)

## 光源设置

本案例中，选择“端口”在波导中注入模式光源。对于双直波导微环谐振腔，添加四个对应的端口来记录输入和输出的仿真数据，用于进一步计算 S 参数等。注意，需要在端口组中选择作为源的端口并设置光源波段，用于求解直波导的注入模式并导入模式源。

![ring_port_1.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/ring_port_1.png)

# 仿真结果

在所有设置均完成之后，便可以开始运行仿真。仿真控制平台可以选择保存实时传输场，方便用户实时观测谐振现象，如下图所示。

![ring_data_t.gif](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/transient_fields_ring.gif)

仿真结束后，Mode Port 和 Monitor 会自动保存观测到的信息。对应的数据可视化界面可获得全部数据信息。更多内容见[数据可视化](/localhost/knowledge-base/User-Manual_data-visualizing)功能介绍。

各端口 Mode Port 数据列表中的 T 展示了波长与透射之间的关系，结果如下图所示。可以明显看到包含$1.55 \mu m$光波在内的三个共振峰。

![ring_fdfp_data_t.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/ring_fdfp_data_t4.png)

根据输出端口的共振峰，查看 FDFP monitor ZX 的数据。波长等于$1.550 \mu m$时对应的电场强度如下图右所示。很明显，相对于非共振波长$1.54 \mu m$（下图左），场值明显增强。

![ring_fdfp_data_e.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/ring_fdfp_data_e2.png)

注：仿真结束后，本软件支持使用脚本查看结果和数据后处理，附件有本案例数据可视化脚本文件。

使用分析组“high Q analysis”可以分析微环谐振腔内三个共振峰的 Q 值。附件工程中已添加对应的分析组，仿真运行完成后可以得到三个共振峰的具体数值和 Q 值，结果如下所示。

```msf
val =
Resonance 1:
val =
    frequency = 196.995THz, or 1521.83 nm
val =
    Q = 3608.12
val =
Resonance 2:
val =
    frequency = 189.921THz, or 1578.51 nm
val =
    Q = 1994.18
val =
Resonance 3:
val =
    frequency = 193.43THz, or 1549.88 nm
val =
    Q = 2672.63
```

# 参考文献

[1] Mirza, Asif , et al. "Silicon Photonic Microring Resonators: Design Optimization Under Fabrication Non-Uniformity." Design, Automation and Test in Europe Conference and Exhibition 2020.
[2] 周治平. 硅基光电子学. 北京大学出版社, 2012.
[3] Hammer, Manfred , K. R. Hiremath , and R. Stoffer . "Analytical Approaches to the Description of Optical Microresonator Devices." Aip Conference Proceedings (2004).
