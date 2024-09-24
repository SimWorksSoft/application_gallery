---
title: 反射型滤色器
description: 人眼会对特定的光谱产生特定的色觉。反射型滤色器，通过选择性的调控反射光谱使人眼获得不同的色觉。本案例展示了如何计算反射光谱对应的色度坐标，并分析了该滤色器的显色调节规律。
language: zh-CN
businessId: reflective-color-filters
keywords: 时域有限差分(FDTD),非对称法布里-珀罗腔,反射型滤色器
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/Reflective_Color_Filters_structures_mpps_20240119150238A053.jpg
---

# 前言

人眼对特定的光谱产生特定的色觉。反射型滤色器，通过选择性的调控反射光谱使人眼获得不同的色觉。参考 Yang[^1]等人的工作，建模仿真了$Ni$/$SiO_2$/$Al$非对称法布里-珀罗（Fabry–Perot，FP）腔的反射型滤色器。其中$Ni$层在太阳光谱范围具有接近完美的吸收（Near-perfect Absorption）效应；选择合适的$Al$层厚度，以阻挡透射；而调整中间层$SiO_2$的厚度，反射光谱将在人眼中产生丰富的高饱和度、高亮度的色觉。本案例展示了如何计算反射光谱对应的色度坐标，并分析了该滤色器的显色调节规律。

# 仿真设置

本案例使用 2D FDTD 仿真，该滤色器为简单的三层薄膜结构，顶层为$Ni$，中间层为$SiO_2$，底层为$Al$，使用$0.38\mu m$~$0.78\mu m$波段的平面光源，沿 z 轴的负方向垂直入射，来模拟自然光照明，如下图所示。由于结构在 x 轴方向周期展开，且源的偏振与 x 轴方向平行，因此，将`X axis min`和`X axis max`设置`Anti-Symmetric`边界以加速仿真计算。需要注意的是，由于顶层$Ni$的厚度较薄，在该层使用自定义网格以细化仿真网格，提高仿真结果的精度。

![structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Reflective_Color_Filters_structures_mpps.png)

| 参数名称 |   尺寸   |
| :------: | :------: |
|   $t$    |  $6 nm$  |
|   $d$    | $120 nm$ |
|   $h$    | $100 nm$ |

## 材料设置

- **$Ni$**
  顶层材料来自内置材料库，需要拟合，拟合波段为可见光波段($0.38\mu m$~$0.78\mu m$)，拟合结果所下图所示。

![Ni](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Reflective_Color_Filters_material_Ni_fit.png)

- **$SiO_2$**
  中间层为$SiO_2$，在$0.38um$~$0.78um$波段可近似为介质（Dielectric）材料，折射率为$1.46$。

- **$Al$**
  底层材料来自内置材料库，需要拟合，拟合波段为可见光波段($0.38\mu m$~$0.78\mu m$)，拟合结果所下图所示。

![Al](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Reflective_Color_Filters_material_Al_fit.png)

# 仿真结果

打开并运行附件工程，在`FDFP Monitor`监视器当中可以得到$0.38\mu m$~$0.78\mu m$全波段的电磁场以及功率等物理量，其中在波长$0.38\mu m$下的电场分布如下图所示，可以看到，由于 FP 腔效应产生的电场局域增强，使得几乎所有的能量被顶层$Ni$吸收，呈现接近完美的吸收效应。同时由于$Al$层的阻挡透射的作用，将电磁波限制在非对称法布里-珀罗腔内。

![FDFP_monitor](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Reflective_Color_Filters_FDFP_monitor.png)

# 参数分析 e

## 反射率谱和色度图坐标

打开附件工程，运行`d_120_270_50nm`参数扫描，设置中间层$SiO_2$的厚度$d$分别为$120nm$、$170nm$、$220nm$、$270nm$，其反射率扫描结果如下图所示。运行脚本`Reflective_Color_Filters.msf`，根据反射率谱，计算得到对应的 CIE 色度坐标，查找色度坐标对应的颜色如图中所示，同时计算反射率谱的波峰分别对应$0.395\mu m$、$0.535\mu m$、$0.676\mu m$、$0.417\mu m$，上述结果与**参考文献 Figure 1**一致。

![ref_sepectrum](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Reflective_Color_Filters_ref_spectrum_4.png)

## 反射率谱随中间层的厚度扫描

打开附件工程，运行`d_50_400_10nm`参数扫描，可以得到反射率谱$R$随$SiO_2$层厚度$d$的连续变化关系，如下图所示。当厚度$d$在$50nm$ - $80nm$时，在可见光波段反射率较低。当厚度$d$从$80nm$连续增加到$240nm$时，反射峰的位置从$0.38\mu m$红移到$0.78\mu m$。此外，当厚度$d$超过$250nm$和$360nm$时，两个高阶模式开始出现在$0.38\mu m$处。该结果与**参考文献 Figure 2**一致。
因此，通过改变中间层$SiO_2$的厚度$d$，反射峰的位置能够得到连续细调，即该滤色器可以获得覆盖整个可见光范围且具有高饱和度和亮度的色彩。

![ref_sepectrum_sweep](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Reflective_Color_Filters_ref_sweep.png)

# 附录

色度图的轮廓覆盖区显示了自然界一切物理可能颜色的色域范围。根据国际照明委员会（International Commission on illumination，CIE）建立的 CIE 标准色度学系统，反射光谱的色度坐标计算如下：

光谱功率分布为:
$$P(\lambda)=I(\lambda)R(\lambda)$$

$I$($\lambda$)是白光光源的相对辐射光谱，$R$($\lambda$)是反射光谱。三刺激值$X$、$Y$和$Z$是通过以下方法计算的：

$$X=\frac{1}{K}\int_\lambda \bar{x}(\lambda)P(\lambda)d\lambda$$
$$Y=\frac{1}{K}\int_\lambda \bar{y}(\lambda)P(\lambda)d\lambda$$
$$Z=\frac{1}{K}\int_\lambda \bar{z}(\lambda)P(\lambda)d\lambda$$

$\bar{x}$，$\bar{y}$，$\bar{z}$是标准观察者函数。积分为可见光$0.38um$~$0.78um$范围，$K$为归一化常数:

$$K=\int_\lambda \bar{y}(\lambda)I(\lambda)d\lambda$$

CIE 色度坐标($x$，$y$，$z$)可通过归一化得到：
$$x=\frac{X}{X+Y+Z}$$
$$y=\frac{Y}{X+Y+Z}$$
$$z=\frac{Z}{X+Y+Z}=1-x-y$$

由于对入射光源的强度进行了归一化处理，（$x$，$y$，$z$）只有两个值是独立的。

# 参考文献

[^1]: Yang Z , Zhou Y , Chen Y , et al. "Reflective Color Filters and Monolithic Color Printing Based on Asymmetric Fabry–Perot Cavities Using Nickel as a Broadband Absorber".Advanced Optical Materials,(2016)
