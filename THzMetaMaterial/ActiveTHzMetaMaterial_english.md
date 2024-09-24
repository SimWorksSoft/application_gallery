---
title: THz Metamaterial
description: Metamaterial is a man-made material with special properties that is not found in nature. This material can regulate basic physical characteristics such as frequency, amplitude, phase and polarization of electromagnetic waves. This case simulates the passive metamaterial described in the paper Chen et al.
language: en-US
businessId: thz-metamaterial
keywords: Finite Difference Time Domain(FDTD),THz metamaterial,Surface current density
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/Active_THz_Metamaterial_structure_20240117165143A048.jpg
---

# Preface

"Metamaterial" is a man-made material with special properties that is not found in nature. This material can regulate basic physical characteristics such as frequency, amplitude, phase and polarization of electromagnetic waves. THz metamaterials are metamaterials that regulate electromagnetic waves with frequencies in the terahertz range. This case simulates the passive metamaterial described in the paper _Chen_ et al. _Active terahertz metamaterial devices[^1]_ and analyzes the surface current density of the metamaterial.

# Simulation settings

## Device introduction

The THz metamaterial used in this case consists of a gallium arsenide (GaAs) substrate and a gold (Au) layer on its surface. Its structure is shown in the figure below. The thickness of gold used in the reference is $0.2 \mu m$, which is much smaller than the wavelength used in the simulation (130$\mu m$ - 1200$\mu m$), so `2D Structure` can be used in this case to build the gold layer. Since the simulation structure and the source are symmetrical in the X direction, we use `Symmetric` boundary conditions in the $X_{min}$ and $X_{max}$ directions.

![Active_THz_Metamaterial_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Active_THz_Metamaterial_structure.png)
|Parameters|A|D|G|W|
|:-----:|:-----:|:-----:|:-----:|:-----:|
|Value ($\mu m$)|36|10|2|4|

## Material

The gold material is represented with the Drude model (which contains the plasma frequency $\omega_p$ and the collision frequency $\gamma_p$). At the low frequency limit ($\omega_p << \gamma_p$), the Drude model can be expressed as a simple conductive model, so this case uses the `Perfect electric condutor(PEC)` instead of gold.

# Simulation results

## Reflectivity and transmissivity

According to the T data obtained by the `Frequency-Domain Field and Power(FDFP)` monitors on the top and bottom of the device, the reflectivity (R) and transmissivity (T) of the structure are plotted as a function of frequency as follows. It can be seen that the resonance frequencies of the metamaterial device are approximately 0.66THz and 1.7THz, which are consistent with the results of the reference as shown in **Figure3a**.

![Active_THz_Metamaterial_RT](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Active_THz_Metamaterial_RT.png)

## Electric field distribution and surface current density

The figure below shows the electric field distribution and the surface current density distribution on the surface of the metamaterial device when the resonance frequency is 0.66THz, plotted using the script file in the attachment. It can be seen from the figure that at the resonant frequency of 0.66THz, the electric field is highly concentrated at the split gap, and there is no obvious surface current on the metal wires connecting the metasurface cells.

![Active_THz_Metamaterial_E](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Active_THz_Metamaterial_E.png)![Active_THz_Metamaterial_K](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Active_THz_Metamaterial_K.png)

# References

[^1]: H.-T. Chen et al., "Active terahertz metamaterial devices", Nature 444, 597-600 (2006)
