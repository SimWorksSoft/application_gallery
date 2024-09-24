---
title: 回音壁模式微盘
description: 回音壁模式微盘是利用光的全反射，将光限制在微盘内，实现光增强的结构。回音壁模式微盘具有很高的品质因子和很小的模式体积，是当前光学研究的一个前沿和热门领域。本案例中，我们希望找到氮化镓圆柱体的一阶和二阶回音壁模式。
language: zh-CN
businessId: whispering-gallery-modes-of-a-microdisk
keywords: 时域有限差分(FDTD),谐振器,回音壁模式(WGMs)
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/WhisperGalleryMicrodisk_Structure_2_20240122092723A058.jpg
---

# 前言

回音壁模式微盘是利用光的全反射，将光限制在微盘内，实现光增强的结构。简单来说，光在高折射率的介质腔内传播时，由于介质腔与外界的折射率差，光线将会在介质边缘处发生全反射。当光绕介质边缘传播一周回到原来的位置时，满足相位匹配条件的光将得到增强。回音壁模式微盘具有很高的品质因子和很小的模式体积，因而在光学探测、非线性光学、腔光力学以及量子光学等诸多方面有重要应用，是当前光学研究的一个前沿和热门领域。本案例中，我们希望找到氮化镓圆柱体的一阶和二阶回音壁模式，重现*Tamboli* 等人在*Room-temperature continuous-wave lasing in GaN/InGaN microdisks[^1]* 论文中的结果。

![WhisperGalleryMicrodisk_Structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/WhisperGalleryMicrodisk_Structure.png)

# 仿真设置

为了避免严重的干涉相消现象，本例中偶极子光源不能选择高度对称的位置，必须随机分布。一般来讲，对时间监视器的电场信号做傅里叶变换可以找到结构的共振频率，但由于本例中的氮化镓圆盘为高 Q 值器件，时域电场信号在模拟结束时不会完全衰减，因此我们使用`FDFP`频域场-功率监视器获得的频谱信息来寻找结构的共振频率。为了避免高 Q 值器件在仿真开始/结束时发生的瞬变，`FDFP`监视器需使用`Full`切趾功能。

# 仿真结果

下图显示了`FDFP`监视器中得到的光谱，从图中可以看出，共振波长分别为$404.7nm、412.2nm、428.5nm、441.3nm$。如果想要获得更加准确的结果，可以使用更加精细的网格。

![WhisperGalleryMicrodisk_E](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/WhisperGalleryMicrodisk_E.png)

下图分别为共振波长为$418nm$和$428nm$时微盘的磁场分布。可以看出共振波长为$418nm$时为微盘的一阶模，共振波长为$428nm$时为微盘的二阶模。该仿真结果与参考文献中**Figure4**给出的结果一致。

![WhisperGalleryMicrodisk_H418](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/WhisperGalleryMicrodisk_H418.png)![WhisperGalleryMicrodisk_H428](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/WhisperGalleryMicrodisk_H428.png)

# 参考文献

[^1]: A. C. Tamboli, E.D. Haberer, R. Sharma, K. H. Lee, S. Nakamura and E. L. Hu, Room-temperature continuous-wave lasing in GaN/InGaN microdisks, Nature Photonics, v1, pp. 61–64 (2007)
