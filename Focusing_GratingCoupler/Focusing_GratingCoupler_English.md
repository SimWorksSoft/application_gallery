---
title: Focusing Grating Coupler
description: One important issue of silicon photonic circuit is an interface between integrated waveguide devices and optical fibers or free-space optics. Grating couplers have the advantages of easy fabrication, high flexibility, and large alignment tolerance, which makes them the most important solution to solve the coupling issues. In this example, we simulate a focusing grating coupler to study its coupling capability.
language: en-US
businessId: focusing-grating-coupler
keywords: Finite Difference Time Domain(FDTD),Focusing grating coupler,Parameter analyses
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/focusingGratingCoupler_E146_20240304132515A020.jpg
---

# Preface

In many fields of data communication, high-speed optical interconnection technology is essential for huge data exchange, and thus the integration of optical interconnection has been a hot research topic in recent years. The leading candidate technology is silicon photonic circuits due to its superior performance, low cost, and monolithic integration with other optoelectronic components. One important issue of silicon photonic circuit is an interface between integrated waveguide devices and optical fibers or free-space optics. Grating couplers have the advantages of easy fabrication, high flexibility, and large alignment tolerance, which makes them the most important solution to solve the coupling issues. In this example, inspired by the work of $Hoffmann$ and his colleagues[^1], we simulate a focusing grating coupler to study its coupling capability.

![focusingGratingCoupler_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/focusingGratingCoupler_structure.png)

# Simulation settings

## Device introduction

The focusing grating coupler used in this example is based on a shallow-etched $SOI$ silicon substrate with a $Si$ waveguide layer, $SiO_{2}$ cladding on both the top and bottom, and the lowest substrate material is still $Si$, as shown in the figure above. The $Z$ direction is the optical transmission direction, and the thickness direction of the optical waveguide is the $Y$ direction. Since the structure is symmetric in the $X$ direction and the light source is anti-symmetric in the $X$ direction, we use the `Anti-Symmetric` boundary condition in the $X_{min}$ direction.

A confocal grating is used for the coupling grating part, and its process parameters (waveguide thickness, buried oxygen layer thickness, substrate thickness, cladding thickness, and shallow etch depth) are specified based on IME, and the grating period, duty cycle, and taper are designed referring to paper[^1], as shown in the figure below. The grating itself focuses light into a silicon wire waveguide of width $dwg=0.5\mu m$, where the taper has a tensor angle of $\alpha=31.5^{\circ}$ and a $r$ of $19.5\mu m$. In the design, the grating pattern is a concentric circular line, with the center of the circle at the apex of a wedge intersecting the waveguide.
![focusingGratingCoupler_gratingstructure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/focusingGratingCoupler_gratingstructure.png)

| Variables | Period/$\mu m$ | Duty |
| :-------: | :------------: | :--: |
|   Value   |      0.67      | 0.53 |

## Source

The light emitted from a step-type single-mode fiber is incident obliquely on the grating, which can be approximated as the field distribution of a `Gaussian` light source, so a Gaussian light source can be used in this example. It is only necessary to match the beam waist of the Gaussian source to the fiber core and to locate the source in the material of the fiber core. The Gaussian light source does not require mode-solving, so the fiber element model can be omitted and only the Gaussian light source can be placed above the grating structure.

# Simulation results

The electric field distribution at a wavelength of $1.46\mu m$ obtained in the `FDFP` monitor placed inside the focusing grating coupler is shown in the figure below. Clearly, the free-space light from the Gaussian source is coupled by the grating into the silicon wire waveguide on the right.
![focusingGratingCoupler_E146](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/focusingGratingCoupler_Efield.png)

The figure displays the transmittance distribution with wavelength obtained from the 'FDFP' monitor in the silicon wire waveguide when the Gaussian light source is $23 \mu m$ away from the silicon wire waveguide. It is evident that the focusing grating coupler achieves a maximum transmittance of $52\%$ at a wavelength of $1.56 \mu m$.
![focusingGratingCoupler_T](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/focusingGratingCoupler_T.png)

# Parameter analyses

The project includes a parameterized sweep that scans the Gaussian source from $23\mu m$ to $25\mu m$ away from the silicon wire waveguide in the optical propagation direction. After the sweep, you can obtain the distribution of transmittance T varying with the position of the light source. The figure shows that the maximum transmittance of the focusing grating coupler is achieved at a wavelength of $1.556\mu m$ when the light source is $24.33\mu m$ away from the silicon wire waveguide, with a T value of $51.97\%$.
![focusingGratingCoupler_sweep](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/focusingGratingCoupler_sweep.png)

# References

[^1]: Hoffmann J ,Schulz M K ,Pitruzzello G , et al.Backscattering design for a focusing grating coupler with fully etched slots for transverse magnetic modes[J].Scientific Reports,2018,8(1):1-8.
