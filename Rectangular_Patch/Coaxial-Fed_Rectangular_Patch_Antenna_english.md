---
title: Coaxial-Fed Rectangular Patch Antenna
description: Coaxial-fed rectangular patch antenna is a fundamental type of microstrip antenna composed of a dielectric substrate, a ground plane, and a conductive patch. Compared to traditional antennas, Coaxial-fed rectangular patch antennas are compact, lightweight, easy to integrate, cost-effective, and suitable for mass production. In this case, a rectangular patch antenna mounted on an infinite metal ground plane is simulated using FDTD, and its return loss and far-field directivity are calculated.
language: en-US
businessId: Coaxial-Fed-Rectangular-Patch-Antenna
keywords: Finite Difference Time Domain(FDTD),Radio Frequency,Antenna
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Rectangular_patch_structure.png
---

# Preface
A patch antenna is a fundamental type of microstrip antenna composed of a dielectric substrate, a ground plane, and a conductive patch. Typically, it is fed using microstrip lines or coaxial cables, exciting an RF electromagnetic field between the conductive patch and the ground plane. The radiation occurs through the gap between the patch and the surrounding ground plane. Compared to traditional antennas, patch antennas are compact, lightweight, easy to integrate, cost-effective, and suitable for mass production. In this case, we use FDTD to simulate the rectangular patch antenna based on *Balanis[^1]* as shown below. First, we determine the resonant frequency, and then, with the assistance of a `Directivity` analysis group, we analyze the antenna’s return loss, directivity, and far-field pattern.

![structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Rectangular_patch_Structure.png)

# Simulation settings
## Device introduction

The patch antenna is constructed from a 2D rectangular sheet of width $11.86 mm$ and length $9.06 mm$ that is mounted onto a rectangular substrate with a refractive index of 1.48, as shown above. The substrate is backed underneath by a ground plane constructed from a 2D rectangular sheet, which extends out of the simulation region, rendering infinite. 

Since the coaxial waveguide’s model intersects the ground plane at z=0 and its inner conductor passes through the substrate, we need to manually specify the `Mesh Order` for these objects to determine the material to be used in the overlapped region, with larger values having higher priority. The `Mesh Order` is assigned as follows: Inner conductor of coaxial waveguide = 2, Outer conductor of coaxial waveguide = 1, Substrate (and coaxial medium) = 0. Since 2d objects always take priority over 3d objects. So there is no need to specify the mesh order of the 2D structure in this case. For specific details on the setup of the `Mesh Order`, please refer to [Mesh order](/localhost/knowledge-base/User-Manual_structures?anchor=58).

The wavelength range of the light source in this case is $24-37 mm$ which is very large compared to the antenna structure, so the default `mesh accuracy` is not sufficient for the simulation. Therefore, we add a fine mesh  on the rectangular substrate of the antenna, and the mesh accuracy of 4 is used for the rest of the simulation region. The following figure shows the index_x distribution obtained from the Index monitor at Y=0 in the XZ plane, and it can be seen that the structure is correctly constructed.

![index_x_XZ](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Rectangular_patch_index_x_XZ.png)

## Directivity analysis group
The Directivity analysis group is used to set up the monitors and find the directivity of the monopole antenna. Since an infinite ground plane is used here, the `inf_ground_plane` variable in the `Setup Variables` tab of the analysis group should be set to 1. You can find out how to calculate the directivity of a dipole source radiating on an infinite ground plane by clicking on [Far Field Analysis - Directivity](/localhost/case-detail/far-field-analysis-directivity).

# Simulation results
## Reflection
After opening the *rectangular_patch.mpps* and running the simulation, the *rectangular_patch.msf* script is used to generate the patch antenna’s performance and radiation properties. The reflection (return loss = 10log10|S11|) seen from port 1 (S11) in the coaxial waveguide is shown below. It can be seen that the resonant frequency of the simulated patch antenna is $9.96 GHz$, which is $0.4\%$ different from the theoretical resonant frequency of $10 GHz$.

![loss](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Rectangular_patch_loss.png)

*rectangular_patch.msf* can also calculate the input impedance of the antenna, as it shown below. It can be seen that the input impedance of the antenna reaches $40.96 \Omega$ at the resonant frequency.

![impedance](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Rectangular_patch_impedance.png)

## Directivity
The directivity analysis group is used to calculate the farfields at the resonant frequency. The *rectangular_patch.msf* script generates plots of the antenna’s directivity in the E-plane (X-Z cut) and H-plane (Y-Z cut) and compares them to theory[^1]. In the E-plane, the $D_{\theta}$ between theory and FDTD general match, the $D_{\theta}$ is well below -80 dB in the E-plane, matching the theory.

![directivity_E](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Rectangular_patch_directivity_E.png)

In the H-plane, the simulation results are very close to the $D_{\phi}$ obtained from theory, as follows.

![directivity_H](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Rectangular_patch_directivity_H.png)

The directivity of the E-plane as well as the H-plane can be plotted in polar coordinates as follows. The asymmetry of the E-plane is due to the asymmetry of the feed position along the ZX-plane.

![directivity_pattern](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Rectangular_patch_directivity_pattern.png)

## Radiation performance
After running the *rectangular_patch.msf* script the radiation performance of the antenna will be automatically displayed in the script console window with the following results:

```msf
============Radiation Performance==============
Resonant Frequency: 9.96 GHz
Input Power: 2.52 nW
Accepted Power: 2.5 nW
Radiated Power: 2.5 nW
Radiation Efficiency from Input Power: 99 Percent
Radiation Efficiency from Accepted Power: 100 Percent
Maximum Directivity: 7.88 dB
Total Realized Gain: 7.84 dB
=======================================
```
The input power and accepted power are equal due to the extremely small value of $S11$ at the resonant frequency. As a result, both definitions of radiation efficiencies are roughly the same value.

# References

[^1]: C. A. Balanis, Antenna Theory and Design, 4th Edition. John Wiley & Sons (2016).