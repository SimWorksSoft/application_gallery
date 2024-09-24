---
title: 能激发塔姆等离激元的光栅
description: 在2007年，Kaliteevski等人在金属和布拉格光栅之间成功激发塔姆等离激元。塔姆等离激元的色散曲线位于光锥内，可以直接被激发，同时，其对光的入射角度没有要求并且TE或者TM偏振光都可以激发。这些特性使得其在表面光增强、非线性光学以及激光等领域有着广阔的发展潜力，本案例将仿真研究该过程。
language: zh-CN
businessId: tamm-plasmon-polaritons-generated-by-bragg-grating
keywords: 时域有限差分(FDTD),布拉格光栅,塔姆等离激元
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/TPP_on_FDTD_T_with_defect_E_20240301135853A016.jpg
---

# 前言

在 2007 年，Kaliteevski 等人在金属和布拉格光栅之间成功激发塔姆等离激元(Tamm plasmon polaritons, TPPs)。这种新的光学效应不同于表面等离激元(surface plasmon polaritons, SPPs)，塔姆等离激元的色散曲线位于光锥内，可以直接被激发，同时，其对光的入射角度没有要求并且 TE 或者 TM 偏振光都可以激发，而 SPPs 则仅支持 TM 偏振光激发。这些特性使得其在表面光增强、非线性光学以及激光等领域有着广阔的发展潜力，本案例将仿真研究该过程。

# 仿真设置

本案例使用 2D FDTD 仿真，构建如下图所示结构，在 x 方向上使用`periodic`边界条件，以节省计算时间。金属$Ag$层与布拉格光栅的相关参数参考文献[^1]，设置如下表所示

![structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/TPP_on_FDTD_structure.png)

|        参数名称         | 符号  |   尺寸   |
| :---------------------: | :---: | :------: |
|   $Ag$$&nbsp$$width$    | $d_a$ | $30 nm$  |
|  $SiO_2$$&nbsp$$width$  | $d_A$ | $275 nm$ |
| $Si_3N_4$$&nbsp$$width$ | $d_B$ | $160 nm$ |
| $Al_2O_3$$&nbsp$$width$ | $ds$  | $258 nm$ |
|           $N$           |  $N$  |   $24$   |

## 材料

本案例当中$Ag$为 _Drude_ 材料，其参数设置如下，拟合结果如下图所示。而布拉格光栅当中的$SiO_2$和$Si_3N_4$为普通的介电材料，其相对折射率分别为 1.45 和 2.2[^1]，缺陷层$Al_2O_3$的相对折射率为 1.76。
|参数名称|符号|尺寸|
|:---:|:---:|:---:|
|$Permittivity$|$\varepsilon$|$3.7$|
|$Drude$$&nbsp$$pole$$&nbsp$$frequency$|$\omega_p$|$1.38253338e16rad/s$|
|$Inverse$$&nbsp$$of$$&nbsp$$the$$&nbsp$$pole$$&nbsp$$relaxation$$&nbsp$$time$|$\gamma_p$|$2.73468141e13rad/s$|

![materials_Ag_drude](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/TPP_on_FDTD_materials_Ag_drude.png)

# 仿真结果

在布拉格光栅当中引入 1 层$Al_2O_3$作为缺陷时，会在原本的禁带内形成超窄带滤波器，此时反射光谱结果如下图所示

![T_with_defect](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/TPP_on_FDTD_T_with_defect.png)

此时在 1.5556$\mu m$波段下的电场如下图所示，可以观察到在$Al_2O_3$处产生了共振

![T_with_defect_E](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/TPP_on_FDTD_T_with_defect_E.png)

而不引入$Al_2O_3$缺陷时，其反射光谱如下图所示

![T_with_no_defect](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/TPP_on_FDTD_T_with_no_defect.png)

此时在 1.5556$\mu m$波段下的电场如下图所示，可以观察到光完全被布拉格光栅层吸收了

![T_no_defect_E](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/TPP_on_FDTD_T_no_defect_E.png)

# 参数分析

打开工程运行`sweep_ds`参数扫描，可以得到缺陷$Al_2O_3$的宽度对反射光谱的影响，如下图所示，随着缺陷的宽度增加，其新产生的共振峰的中心波长红移，结果与文献[^1]当中**Fig.3**一致。

![T_sweep_ds](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/TPP_on_FDTD_T_sweep_ds.png)

# 参考文献

[^1]: H Lu,YW Li,H Jia, et al. "Induced reflection in Tamm plasmon systems." Optics Express,27(4): 5383-5392(2019).
