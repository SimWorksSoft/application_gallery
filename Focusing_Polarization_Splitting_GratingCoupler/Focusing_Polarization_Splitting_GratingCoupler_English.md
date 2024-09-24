---
title: Focusing Polarization Splitting Grating Coupler
description: The grating coupler has emerged as crucial components in silicon nanophotonics. Addressing the coupling issue between optical fibers and waveguides has become a prominent research focus in recent years. Polarization splitting grating couplers in this case can simultaneously achieve polarization beam-splitting and light coupling functions, which enables the vertical grating coupling between fibers and Silicon-On-Insulator platform for various polarization states. This approach represents one of the most optimal solutions to tackle this issue.
language: en-US
businessId: focusing-polarization-splitting-grating-coupler
keywords: Finite Difference Time Domain(FDTD),Focusing grating coupler,Polarization beam splitter
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/polarization_slitting_grating_coupler_result_20240304132421A019.jpg
---

# Preface

With SOI platform widely used in the integrated optics, the grating coupler has emerged as crucial components in silicon nanophotonics by virtue of its advantages of easy processing, easy alignment and easy integration. The polarization state of light in optical fibers is often difficult to determine, at the same time, the grating coupler is highly sensitive to the polarization of light, and there are significant differences in coupling efficiency for different polarization states of light. Therefore, addressing the coupling issue between optical fibers and waveguides has become a prominent research focus in recent years. Polarization splitting grating couplers can simultaneously achieve polarization beam-splitting and light coupling functions, which enables the vertical grating coupling between fibers and SOI platform for various polarization states. This approach represents one of the most optimal solutions to tackle this issue.

Based on the work of Frederik et al.[^1], a two-dimensional (2D) focusing polarization splitter grating coupler is constructed. The standard 2D focusing polarization splitting grating coupler can be considered as the approximate superposition of two 1D focused grating couplers placed orthogonally. The incident direction of the fiber is perpendicular to the plane of the grating coupler. After polarization selection by the grating coupler, the incident light is focused into two different output ports, as shown in the following figure.

![polarization_slitting_grating_coupler_hole](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/polarization_slitting_grating_coupler_hole.png)

# Simulation settings

## Device introduction

The simulation structure in 3D FDTD is shown in the following figure. It is effective to add a sector structure between the grating coupler and the output waveguide to reduce the coupling loss. The entire grating coupler is based on the SOI platform that has a three-layer structure. The bottom layer is $Si$ , the middle layer is $SiO_2$ , and the upper layer is placed with $Si$ optical waveguide devices. In this example, the grating coupler is composed of a series of air holes etched on the $Si$ substrate. The center of the circular hole is located at the intersection of two 1D focusing grating lines. The relevant parameters are shown in the table below according to ref[^1].

|             name             |      size      |
| :--------------------------: | :------------: |
| $Waveguide$ $&nbsp$ $Length$ |   $15 \mu m$   |
| $Waveguide$ $&nbsp$ $Depth$  |  $0.22 \mu m$  |
|    $Hole$ $&nbsp$ $Depth$    |  $0.07 \mu m$  |
|   $Hole$ $&nbsp$ $Radius$    | $0.1825 \mu m$ |
|             $L$              |  $25.5\mu m$   |

![structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/polarization_slitting_grating_coupler_structure.png)

## Source

In this case, Gaussian source is used to simulate the fundamental mode in optical fiber. The source is tilted to minimize reflection. The waist radius and tilt angle of the Gaussian light source are set as follows. The electric field of the source is shown in the following figure.

|               name                |    size     |
| :-------------------------------: | :---------: |
|      $Waist$ $&nbsp$ $Width$      | $4.6 \mu m$ |
|      $Angle$ $&nbsp$ $Theta$      |   $-10^o$   |
|       $Angle$ $&nbsp$ $Phi$       |   $45^o$    |
| $Linearly$ $&nbsp$ $Polarization$ |   $90^o$    |

![source](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/polarization_slitting_grating_coupler_source.png)

# Simulation results

After opening and running the attached project, it can be observed that the light is equally divided into two output ports at the 1.5$\mu m$.

![result](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/polarization_slitting_grating_coupler_result.png)

The following results can be obtained by running the script `focusing_grading_plot`. In the graph, the transmittance of both output ports is equal, and the total of T1 and T2 exceeds 0.34.
![T1_T2](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/polarization_slitting_grating_coupler__T.png)

# Parameter analyses

By running parameters sweep, we can observe the relation between the transmittance of the two ports and the polarization angle of the source. As the polarization angle shifts from 45 degrees to 135 degrees, the light switches from one output port (e.g.,T2) to the other (e.g.,T1).

![T1_sweep](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/polarization_slitting_grating_coupler_T1_sweep.png)
![T2_sweep](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/polarization_slitting_grating_coupler_T2_sweep.png)

# References

[^1]: Frederik Van Laere , Wim Bogaerts , Pieter Dumon , et al."Focusing Polarization Diversity Grating Couplers in Silicon-on-Insulator." JOURNAL OF LIGHTWAVE TECHNOLOGY, VOL. 27, NO. 5, MARCH 1, 2009
