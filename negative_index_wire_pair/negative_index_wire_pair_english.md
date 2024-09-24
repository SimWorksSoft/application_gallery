---
title: Negative Index Metamaterial Using Wire Pairs
description: Negative index metamaterial (NIM) refers to an artificial optical structure whose refractive index is negative for electromagnetic waves within a certain frequency range. The purpose of this article is to simulate and explain the metamaterial structure described in the paper written by J. Zhou.
language: en-US
businessId: negative-index-metamaterial-using-wire-pairs
keywords: Finite Difference Time Domain(FDTD),Negative index metamaterial,Plasmonic
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/Negative_index_metamaterial_structure_20240119145619A052.jpg
---

# Preface

Negative index metamaterial (NIM) refers to an artificial optical structure whose refractive index is negative for electromagnetic waves within a certain frequency range. The purpose of this article is to simulate and explain the metamaterial structure described in the paper written by J. Zhou. The above-mentioned reference examines the use of multiple copper wire pairs isolated by a dielectric layer with a thickness denoted as $ts$. The individual periodic unit is illustrated in the following figure.

![negative_metamaterial_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Negative_index_metamaterial_structure.png)

# Simulation Settings

In 3D FDTD, the wire pair structure is built based on the parameters given in the reference as shown in the figure below. Where, a planar source with a frequency of 12-16 GHz is used to study the transmissivity and reflectivity of this structure. For the dielectric layer, the thickness ($ts$) is 254 $\mu m$ and the relative permittivity is 2.53. Both the upper and lower sides of the dielectric layer are covered by copper wire pairs with a thickness of 10 um. Within the frequency range of 12-16 GHz, copper behaves similarly to a perfect conductor due to its relative permittivity involving an extremely large imaginary part. Therefore, a perfect electrical conductor (PEC) is used as a substitute for metallic copper. Furthermore, accurate simulation of a 10um thick copper layer requires a fine mesh in the Z direction, leading to increased memory usage and extended computation time. However, a 2D structure can be used instead of a 3D structure to maintain the accuracy of simulation results, while reducing memory and time consumption.

![simulation_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Negative_index_simulation_structure.png)

Since a symmetric periodic structure is used, a combination of symmetric/anti-symmetric conditions can be applied at both boundaries to reduce the simulated space by 3/4 and shorten the simulation time. In this case, "X axis min" and "X axis max" are set to "Symmetric", and "Y axis min" and "Y axis max" are set to "Anti-Symmetric".

# Simulation Results

By running the attached script `negative_index_wire_pair.msf` after the simulation process is completed, the transmission and reflection properties of the structure are obtained. These simulation results closely resemble those reported in the reference [^1].

![transmission](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Negative_index_transmission.png)
![reflection](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Negative_index_reflection.png)

# References

[^1]: Zhou J , Zhang L , Tuttle G , et al. "Negative index materials using simple short wire pairs." Physical Review B, 73(4):041101.(2006)
