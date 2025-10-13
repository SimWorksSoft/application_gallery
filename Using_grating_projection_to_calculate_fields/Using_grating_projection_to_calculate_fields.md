---
title: 使用光栅投影计算任意位置的场
description: 在 FDTD 仿真中，如果需要获取器件较远位置的场分布，通常需要在 FDTD 中扩展计算区域，让光在仿真域内完整传播到目标面。虽然这种方式直观，但会显著增加计算规模和耗时。本案例展示了一种基于光栅投影的方法，可以快速获得在匀质介质中传播的场在任意指定位置的分布，并通过与 FDTD 仿真结果的对比验证其准确性。
language: zh-CN
businessId: using-grating-projections-calculate-fields-at-an-arbitrary-location
keywords: 时域有限差分(FDTD),光栅投影
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Using_GP_calculate_fields_newcover.jpg
---

# 前言
在 FDTD 仿真中，获取器件远场分布通常有两种主流方法：一种是直接扩大仿真区域，使光传播至目标位置，这种方式虽然直观，但计算成本较高；另一种是近场-远场变换，该方法无需扩展仿真域，适用于快速估算远场行为。然而，对于周期性结构（如光栅），普通的近远场变换在处理复杂衍射级次的传播与干涉时存在局限。为此可以采用光栅投影方法，将器件近场信息分解为不同方向的平面波，进而准确重构其在均匀介质中传播至任意远场位置的结果。本案例演示了如何借助光栅投影快速计算指定远场区域的场分布，并通过与标准FDTD结果对比，验证了该方法的可靠性。

# 仿真设置
## 模型简介
本案例所用模型以玻璃为基底，其上表面覆盖一层金薄膜，金薄膜中间刻蚀有一个半径为 $r=0.2\ \mu m$ 的孔。结构在$X、Y$方向上的周期均为$1.5\ \mu m$。平面波光源的波长范围为 $0.4-0.6\ \mu m$，沿 $Z$ 轴正向从玻璃基底入射，电场沿 $X$ 轴方向振动。根据光源和结构的对称性，在$X$和$Y$方向分别使用`Anti-Symmetric`和`Symmetric`边界条件，将仿真区域缩小至原来的$1/4$。在使用对称/反对称边界模拟周期结构时，应确保对应方向的最大边界和最小边界同时设置为相应的边界类型。

![simulation](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Using_GP_calculate_fields_simulation.png)

# 仿真结果
运行附件中的 *solvers_propagate_periodic.msf* 脚本，可以调用`grating`系列函数进行光栅投影，将结构上方 $0.12\ \mu m$ 处 `FDFP` 监视器记录的电场分解为一系列平面波，然后将这些衍射平面波按照波矢关系投影到目标面，得到该位置的电场分布。下图显示了在 $Y=0$ 平面上，光传播到结构上方 $10.5\ \mu m$ 处波长为$500\ nm$的传播电场强度分布，其中左侧为 `FDFP` 监视器获得的结果，右图为通过光栅投影计算得到的结果。

![E2_transmission](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Using_GP_calculate_fields_E2_transmission.png)

下图展示了沿 $(x,y)=(0,0)$ 位置的电场强度以及 $E_x$ 分量的对比结果。可以看到，投影得到的结果与 FDTD 仿真得到的结果基本一致。

![E2_compare](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Using_GP_calculate_fields_E2_compare.png)

![Ex_compare](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Using_GP_calculate_fields_Ex_compare.png)

值得注意的是，光栅投影法同样适用于倾斜入射的情况。下图展示了在入射角为 $10\degree$ 时，利用该方法得到的电场分布。需要注意的是，在进行倾斜入射仿真时，应将 $X$ 和 $Y$ 方向的边界条件设置为 `bloch`。

![E2_theta_10](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Using_GP_calculate_fields_E2_theta_10.png)

![E2_compare_theta_10](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Using_GP_calculate_fields_E2_compare_theta_10.png)

![Ex_compare_theta_10](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Using_GP_calculate_fields_Ex_compare_theta_10.png)

从图中可以看出，即使在倾斜入射情况下，投影计算的结果仍与 FDTD 仿真吻合。但随着传播距离增加，两者之间的差异逐渐增大，这是由于 FDTD 仿真存在网格色散效应：网格上的光速与自由空间存在微小差异，并呈现各向异性。因此，对于长距离传播而言，投影结果实际上更加精确。

下图展示了使用投影法得到的波长为$500\ nm$光场，传播距离达到 $100\ \mu m$。您可以将 *solvers_propagate_periodic.msf* 脚本中的 `test` 设置为0，并重新运行脚本以获得该结果。

![E2_100um](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Using_GP_calculate_fields_E2_100um.png)

# 附录
## 光栅投影
光栅投影是一种基于角谱理论和弗洛奎特-布洛赫定理的高效数值方法，专门用于处理周期性结构的光场传播问题。该方法将监视器中记录的近场分布按照光栅方程分解为一系列离散的衍射平面波，通过计算这些平面波在均匀介质中的传播，可以准确重构出任意指定位置处的场分布。
### 基本原理
对于二维周期性结构，其衍射波矢满足光栅方程：

$$k_{x}^{n}=k_{x}^{in}+n\frac{2\pi}{ax}$$
$$k_{y}^{m}=k_{x}^{in}+m\frac{2\pi}{ay}$$

其中$k_{x}^{n}$和$k_{y}^{m}$分别是第 $(n,m)$ 级衍射光相关的面内波矢，$ax$和$ay$分别为$x$和$y$方向上的周期。$k_{x}^{in}$ 和 $k_{y}^{in}$ 为入射波矢分量。

在已知近场分布$E(x, y, z_0)$ 的情况下，可将其分解为一系列平面波的叠加：

$$E(x,y,z_0)=\sum_{n,m} E(n,m)exp(i(k_{x}^{n}x+k_{y}^{m}y))$$

其中系数$E(n,m)$系数表示第 $(n,m)$ 级衍射平面的复振幅，可通过 `gratingvector` 函数计算获得。

### 任意位置场分布计算
在均匀介质中，这些平面波传播到任意位置 $z = z_0 + \Delta z$ 的场分布可通过下式计算：

$$E(x,y,z_0)=\sum_{n,m} E(n,m)exp(i(k_{x}^{n}x+k_{y}^my+k_{z}^{(n,m)}\Delta z))$$

其中$k_{z}^{(n,m)}$ 为第 $(n,m)$ 级衍射的纵向波矢分量：

$$k_z^{(n,m)}=\sqrt{k^2-(k_x^n)^2-(k_y^m)^2}$$

这里 $k_0$ 为自由空间波数。对于传播模式（实数的 $k_z$），该表达式描述相位积累；对于倏逝波（虚数的 $k_z$），则表征指数衰减。