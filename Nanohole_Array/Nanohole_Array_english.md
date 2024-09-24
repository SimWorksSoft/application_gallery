---
title: Nanohole Array
description: The interaction between incident light and surface electrons of a metallic nanostructure leads to surface plasmon resonance (SPR), which exhibits unique optical properties, including out-of-limit diffraction and local field enhancement. This case involves building a model of a metal film structure with air-hole array and calculating the transmission and reflection spectra of the film by the FDTD method to analyze the near-field distribution on the film surface and the local field enhancement caused by SPR.
language: en-US
businessId: nanohole-array
keywords: Finite Difference Time Domain(FDTD),Nanohole array,Surface Plasmon Resonance(SPR)
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/nanohole_array_structures_20240119145000A051.jpg
---

# Preface

The interaction between incident light and surface electrons of a metallic nanostructure leads to surface plasmon resonance (SPR), which exhibits unique optical properties, including out-of-limit diffraction and local field enhancement. This case involves building a model of a metal film structure with air-hole array and calculating the transmission and reflection spectra of the film by the FDTD method to analyze the near-field distribution on the film surface and the local field enhancement caused by SPR.

![structures](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_structures.png)

# Simulation Settings

The 3D FDTD simulation is utilized to build a metal film structure with the periodic hole array, as shown in the figure below. In this case, the metal film is made of gold with a thickness of 100 nm; $ø$ 100 nm cylindrical air holes are distributed with a periodic pitch of 400 nm; and the wavelength of the incident plane light is taken within the range of 400~750 nm. In particular, if the periodic unit exhibits planar symmetry, the minimum and maximum boundary conditions along the corresponding axis in the simulation region can be set to either symmetric or anti-symmetric, which are equivalent to periodic boundary conditions. Since the periodic unit and source used in this case is a symmetric structure, symmetric/anti-symmetric boundary conditions are used instead of periodic boundary conditions in order to reduce computational complexity and improve simulation efficiency. (Note: The selection of symmetric/asymmetric boundaries must be consistent with the polarization of the source. ) In the FDTD simulation, an automatic non-uniform mesh is used in the entire simulation region, and an additional overlay mesh with a higher resolution of 10 nm is particularly applied at the nanohole structure for more accurate simulation results.

![structures](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_simulation_structures.png)

For the metal film material, namely gold, the refractive index is taken from the sample reference given in the `CRC Handbook of Chemistry and Physics`. The simulation model that is fitted according to relevant material data is shown in the figure below, illustrating the trend of refractive index variations in the defined wavelength range. Based on the dispersion relation, the properties of the material within the wavelength range can be estimated.

![material](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_Au_material_fit_1.png)

# Simulation Results

After opening the attached project file and performing the simulation, then running the script file, all the target data are obtained.
The figure below displays the reflection and transmission spectra recorded by the `FDFP monitors` `R` and `T`. The R+T spectra are derived through calculations performed with the script file. In this graph, a significant resonance effect is observed at the wavelength of approximately 675 nm.

![R+T](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_T_and_R_1.png)

As shown in the figure below, the transmission spectrum is normalized by dividing the area of the air hole by that of the periodic cell. This normalization reveals that the transmission is significantly higher than the normal level in certain wavelength ranges.

![cw_T](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_T_normalized_1.png)

The distribution plots of $|E|^2$ at the transmitted and reflected surfaces of the gold film are shown below. Although the intensity in the incident field is only 1$V/m$, a comparison of this intensity with the intensity of the transmission/reflection profiles shows that there is a significant enhancement in the local near-field.

![abs(E)2_T](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_Transmitted_surface_E_1.png)
![abs(E)2_R](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_reflected_surface_E_1.png)

Below is the field distribution of the z-y plane section at x=0. By adjusting the range of the data colorbar, the regions where the near-field intensity has been increased by more than 10 times are clearly displayed.

![abs(E)2](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nanohole_array_zyplane_surface_E_1.png)
