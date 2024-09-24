---
title: Exciting the Surface Plasmon-Polaritons in Graphene
description: The chemical potential of graphene can be regulated by methods such as voltage  or chemical doping. This property makes graphene highly versatile in the field of material-light interactions, particularly in relation to surface plasmon polaritons (SPPs). By exciting surface plasmons, graphene significantly enhances its ability to interact with light.
language: en-US
businessId: exciting-the-surface-plasmon-polaritons-in-graphene
keywords: Finite Difference Time Domain(FDTD),Graphene,Photonic crystal,Plasmonic
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/surface_plasmon_in_graphene_structures_20240119152811A055.jpg
---

# Preface

Graphene, with its excellent electrical, thermal and mechanical properties, has attracted extensive attention from scientific researchers since its discovery. The chemical potential of graphene can be regulated by methods such as voltage or chemical doping. This property makes graphene highly versatile in the field of material-light interactions, particularly in relation to surface plasmon polaritons (SPPs). Surface plasmon polaritons are electromagnetic surface waves in which the field energy is predominantly concentrated on the surface of a metal and decays exponentially in the direction perpendicular to the interface. By exciting surface plasmons, graphene significantly enhances its ability to interact with light.
Based on the work outlined in the reference [^1], this case aims to study the enhanced interaction between graphene and light when graphene satisfies the conditions for surface plasmon resonance.

# Simulation Settings

In this case, as described in the reference, we model the structure shown in the figure below by 2D FDTD. A five-layer photonic crystal (PC) structure is placed on a glass substrate, and a graphene film is overlaid on the surface of this PC structure. The outermost layer is then covered with a layer of PMMA material. Considering the structure extends uniformly and infinitely in the X and Y directions, the thickness in the X direction is artificially taken as 10 nm in this case to minimize the calculation time. Moreover, a plane wave is used as the source and its incident angle will be swept in subsequent steps. Since the plane source involves an incident angle, `bloch` periodic boundary conditions are applied in the X direction to simulate the oblique incidence of the source. For details, see [Bloch Boundary Conditions](/localhost/knowledge-base/User-Manual_boundary-condition-settings).

![structures](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/surface_plasmon_in_graphene_structures.png)

## Material

At a wavelength of 1.31 $\mu m$, the substrate material $SiO_2$ used in this structure has a refractive index of 1.4468. The PC structure consists of alternating layers of $TiO_2$ (refractive index: 2.7204) and $SiO_2$ (refractive index: 1.4468). The topmost layer is made of PMMA with a refractive index of 1.481, and the background material is air with a refractive index of 1. For the graphene material, the scattering rate and chemical potential are set to 0.11 meV and 0.05 eV respectively, as shown in the fitting curve below. For more parameters and details, see [Graphene](/localhost/knowledge-base/User-Manual_graphene-material).

![graphene_fit](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/surface_plasmon_in_graphene_material_fit.png)

# Simulation Results

Open the attached project and run parameter sweep. After the project is completed, run script file `Exciting_TE_SPPs_in_graphene.msf`. The incident angle of the plane wave is scanned within the range of 43° to 51° in the parameter sweep. The results obtained for the transmissivity and reflectivity are shown as below, wherein the reflectivity trend is consistent with Figure 2 in the reference. It can be observed that once the angle of the incident plane wave is aligned with the wavevector of surface plasmon resonance, graphene experiences surface plasmon resonance, resulting in a significant increase in absorption of incident light by graphene. At this specific angle, the transmission and reflection are almost negligible.

![T_and_R](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/surface_plasmon_in_graphene_T_R_new.png)

The script also plots the variation of the electric field in the Z direction as a function of the incident angle, as shown in the figure below. The results indicate that at an angle of 50.5°, there is coupling between the electric field and the graphene layer, leading to an enhancement of the electric field intensity specifically where the graphene layer is present.

![E2](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/surface_plasmon_in_graphene_E2_new.png)

# References

[^1]: I. Degli-Eredi, J. E. Sipe, and N. Vermeulen, “TE-polarized graphene modes sustained by photonic crystal structures”, Opt. Lett. Vol. 40, No. 9, pp. 2076-2079 (2015).
