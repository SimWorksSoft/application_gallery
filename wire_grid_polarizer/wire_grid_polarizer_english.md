---
title: Wire Grid Polarizer
description: Wire grid polarizer(WGP) is a type of polarizer composed of a metallic grating with a sub-wavelength period and typically made of metals such as gold, silver, aluminum. Due to their advantages, including compact structure, high brightness, high polarization extinction ratio (PER), wide field of view, and ease of integration, WGPs can be widely applied in various fields such as photoswitches, optical displays, and imaging systems. This case is based on the work of Ahn et al. By controlling the grating spacing, duty cycle, and Al grating height, the extinction ratio and transmission optical characteristics can be adjusted.
language: en-US
businessId: wire-grid-polarizer
keywords: Finite Difference Time Domain(FDTD),Metallic grating,Wire grid polarizer,Polarization extinction ratio
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/Wire_grid_polarizer_structure_20240119153701A057.jpg
---

# Preface

Wire grid polarizer (WGP) is a type of polarizer composed of a metallic grating with a sub-wavelength period and typically made of metals such as gold, silver, aluminum. Thanks to their advantages, including compact structure, high brightness, high polarization extinction ratio (PER), wide field of view, and ease of integration, WGPs can be widely applied in various fields such as photoswitches, optical displays, and imaging systems. This case aims to replicate the research work conducted by Ahn et al. [^1] The schematic diagram of the structure involved in this case is shown below. The optical properties, e.g., PER and transmission can be adjusted by controlling relevant parameters such as grating pitch, duty cycle, and Al grating height. This case focuses on investigating the transmission properties of a WGP for different polarized light within the visible light range.

![structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Wire_grid_polarizer_structure.png)

# Simulation Settings

As the WGP features a periodic structure, the 2D FDTD simulation is simplified by creating a unit structure and applying `Periodic` boundary conditions to minimize the calculation time. The WGP is composed of a uniform aluminum wire grid with the following dimensions: wire width $W=100nm$ (grating unit pitch $pitch=200nm$), thickness $H=140nm$, and is placed on a glass substrate. The structure is shown in the figure below. For the grating region, a custom mesh $1nm \times 1nm$ is used to improve the accuracy of simulation results.

![structure_simulation](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Wire_grid_polarizer_structure_simulation.png)

- **Material**

  The material of the grating is taken from the built-in material library `Al (Aluminium) - Palik` and is therefore subject to fitting within the wavelength range of $0.45um-0.65um$. The fitting results are shown in the figure below.

![Al_fit](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Wire_grid_polarizer_material_Al_fit.png)

# Simulation Results

The results indicate that the WGP exhibits an extremely high ($90\%$) reflectivity $R$ for TM waves (S-polarization or S-Pol), while it primarily allows transmission (>$75 \%$) for TE waves (P-polarization or P-Pol). By sweeping the transmissivity/reflectivity of the WGP for different grating pitches, the results obtained show that at a wavelength of $450nm$, using a pitch of $100nm$ for the WGP leads to an extremely high PER (>$40000$). This finding is consistent with the results reported in the reference.

## Reflectivity and Transmissivity of TE and TM Polarizations

After opening the attached project and executing `T_TEM` sweep in the Sweep tab, then running the file "TEM_RT_sweep.msf", the reflectivity and transmissivity curves for TE and TM polarizations are plotted.

![TEM_RT](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Wire_grid_polarizer_TEM_RT_new.png)

When the source is incident with TE polarization, more than $75 \%$ of the incident light is transmitted through the system. Conversely, when the light is incident with TM polarization, there is minimal transmission, with approximately $90\%$ of the light being reflected. This demonstrates the polarization selectivity of that WGP for incident light.

## Dependence of PER on Grating Pitch

The figure below is obtained by the following steps: open the attached project, execute `grating_pitch_sweep` in the Sweep tab, run the file `grating_pitch_sweep.msf`, and then set the scale of the y-axis to logarithmic.

![sweep_PER](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Wire_grid_polarizer_sweep_PER_new.png)

The extracted plots show the correlation between the PER and the grating pitch of the WGP at three different wavelengths of $450nm$, $550nm$, and $650nm$ respectively. These results are consistent with **Figure 2** [^1] given in the reference. At a wavelength of $450nm$, the WGP with a grating pitch of $100nm$ achieves a PER up to $40000$.

# Appendixes

## S-polarization and P-polarization

### Definitions

When studying light incident on optical surfaces, it is very common to consider the polarization state of the incident light, specifically whether it is S-polarized or P-polarized. However, there are different definitions regarding S-polarization and P-polarization in various references, which may potentially cause additional ambiguity and confusion for readers trying to understand the concepts. Click [here](https://www.rp-photonics.com/spotlight_2012_03_03.html)[^1] to read more details. For further clarification, the two different definitions are illustrated in the schematic diagrams below.

![sp_polarization](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Wire_grid_polarizer_sp_polarization.png)

The reference [^1] follows the definition shown in the left diagram (conventional definition) to determine S-polarization and P-polarization, which aligns with the definition applied in this case.

### Relationship with TE and TM

TE and TM respectively refer to transverse electric field and transverse magnetic field.
Specifically, it becomes apparent that S-polarization and P-polarization correspond to TM and TE polarizations respectively in 2D simulations when light is incident perpendicular to a surface, according to the conventional definition.

## Polarization Extinction Ratio

### Extinction Ratio

In the field of telecommunications, the extinction ratio (ER) refers to the ratio between two optical powers, which is calculated using the following equation:

$$r_e=\frac{P_{1}}{P_{0}}$$

Where, $P_{1}$ and $P_{0}$ respectively represent the optical power when the source is turned on and the optical power when the source is turned off.
As a dimensionless physical quantity, the ER is typically expressed in dB:

$$r_e=-10log(\frac{P_{1}}{P_{0}})$$

### Polarization Extinction Ratio

The polarization extinction ratio (PER) refers to the ratio between the power of two orthogonally polarized lights. In general, the transmission extinction ratio is calculated using the following equation:

$$r_{pe}=-10log(\frac{P_{s}}{P_{p}})$$

$P_{s}$ and $P_{p}$ respectively represent the optical power of S-polarized light and the optical power of P-polarized light. The PER is expressed in dB.
The total power $P_0$ of the source is a constant value, therefore:

$$r_{pe}=-10log(\frac{P_{s}/P_0}{P_{p}/P_0})=-10log(\frac{T_{s}}{T_{p}})$$

$T_{s}$ and $T_{p}$ respectively represent the transmissivity of S-polarized light and the transmissivity of P-polarized light. The PER is expressed in dB.

Since $T_p$ cannot exceed $100\%$, the most effective way to increase the PER is to reduce $T_S$.

# References

[^1]: Ahn et al,. "Fabrication of a 50 nm half-pitch wire grid polarizer using nanoimprint lithography", Nanotechnology, 16, 1874–1877 (2005)
