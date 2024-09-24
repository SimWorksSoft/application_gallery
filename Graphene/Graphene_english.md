---
title: Tunable Terahertz Metamaterials Based on Graphene
description: Graphene is a single-layer carbon material that is only one atom thick. It can be used in nanoscale plasma systems due to its unique physical properties. Light can be manipulated and controlled by adjusting the electrostatic doping or Fermi level to excite plasmon waves in single-layer graphene. According to the research by Chu et al., slight variations in the number of graphene layers and Fermi level can lead to significant changes in the resonant wavelength and modulation intensity. This case aims to simulate this tuning process in 3D FDTD.
language: en-US
businessId: tunable-terahertz-metamaterials-based-on-graphene
keywords: Finite Difference Time Domain(FDTD),Graphene,Metamaterial,Plasmonic
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/graphene_structure_20240119144030A050.jpg
---

# Preface

Graphene is a single-layer carbon material that is only one atom thick. It can be used in nanoscale plasma systems due to its unique physical properties. Light can be manipulated and controlled by adjusting the electrostatic doping or Fermi level to excite plasmon waves in single-layer graphene.
Chu [^1] et al. studied a type of tunable terahertz metamaterial based on single-layer and multilayer doped graphene. They found that even slight variations in the number of graphene layers and Fermi level may lead to significant changes in the resonant wavelength and modulation intensity. This case aims to simulate this tuning process in 3D FDTD.
![graphene_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/graphene_structure.png)

# Simulation Settings

In this case, graphene is deposited on a silicon substrate with $W=0.15 um$ in X direction and $L=0.01um$ in Y direction respectively. The thickness of the $SiO_2$ substrate is $t=10 um$. Due to the uniform and infinite extension of the structure in the X and Y directions, periodic boundary conditions are applied in X&Y directions to minimize the simulation time. While in the Z direction, PML boundary conditions are used and the PML layer is set to 12 to enhance light absorption. The simulation sketch is shown below. In addition, a custom mesh is used to improve the simulation accuracy.

![graphene_simulation_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/graphene_simulation_structure.png)

## Material

- **Graphene**

  For detailed definitions and settings of graphene parameters, see [Graphene](/localhost/knowledge-base/User-Manual_graphene-material).
  When simulating the graphene metamaterial project, the four parameters, as listed in the table below, are evaluated to explore the changes in the resonant wavelength and modulation depth as the number of graphene layers and Fermi level variation.

| Number | Scattering Rate($\Gamma$) | Chemical Potential($\mu_c$/eV) | Temperature(T/K) | Conductivity Scaling(c) |
| :----: | :-----------------------: | :----------------------------: | :--------------: | :---------------------: |
|   1    |          0.00102          |             0.265              |       300        |            1            |
|   2    |          0.00102          |             0.265              |       300        |            4            |
|   3    |          0.00099          |             0.217              |       300        |            1            |
|   4    |          0.00099          |             0.217              |       300        |            4            |

When the above parameters are set as follows: $Scattering Rate = 0.00099$； $Chemical Potential(eV)  = 0.217$； $Temperature(K) = 300$； $Conductivity Scaling= 1$, the fitting results for the graphene surface conductivity are obtained, with its real and imaginary parts shown in the following figures:

![graphene_material_fit](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/graphene_material_fit_1.png)

# Simulation Results

In this case, the graphene simulation is performed by setting the chemical potential (Fermi level) to 0.265 eV and 0.217 eV, and the number of graphene layers to 1 and 4, respectively. The material parameters are set according to the reference [^1], where graphene is simulated using an approximate Drude model. However, in this case, the graphene is fitted by a full surface conductivity model that involves both intraband and interband conductivities.

After opening the attached project and running the nested parameter sweeps `graph_layers` (Note: in this case, it is necessary to select `Full size` in the `Cloud` option and check `Optimizations and Sweep download children projects` to save the subprojects) , the transmissivity values for different Fermi levels and numbers of graphene layers are obtained (see the figure below), which closely match the results shown in Figure 3(a) of the reference [^1]. The simulation results suggest that increasing the Fermi level of graphene leads to a blue shift in the resonant wavelength, and a higher number of graphene layers also results in an increased modulation intensity.

![transmission](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/graphene_transmission_new.png)

# Appendixes

The graphene conductivity [^1] based on the approximate Drude model:
$$\sigma \approx \frac{-ie^2E_F}{\pi \hbar^2(\omega + i\tau^{-1})}$$
$\omega$ is the angular frequency, $\tau$ is the electron relaxation time, and $E_F$ is the Fermi level.
For the material used in this model, the contribution of interband electronic transitions to the conductivity is omitted. By running the script `Graphene_conductive.msf` upon the completion of the nested parameter sweeps mentioned above, the real and imaginary parts of the graphene surface conductivity are obtained based on the Drude model and the full surface conductivity model, respectively. The graphene materials used in these two models exhibit certain differences in the surface conductivity.

![sigma_real](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/graphene_sigma_difference_real_1.png)
![sigma_imag](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/graphene_sigma_difference_imag_1.png)

# References

[^1]: H. S. Chu, C. H. Gan, "Active plasmonic switching at mid-infrared wavelengths with graphene ribbon arrays," Appl. Phys. Lett. 23,(2013)
