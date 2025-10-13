---
title: Focusing with a single subwavelength aperture
description: Subwavelength optical devices hold great potential in light field manipulation and photonic integration. However, at subwavelength scales, light undergoes strong interference and diffraction, making it difficult to achieve efficient focusing. Garcia-Vidal et al proposed a structure consisting of a single subwavelength aperture in a metallic film surrounded by periodic surface grooves. By exciting surface plasmons, this design enables far-field focusing. In this case, we reproduce the structure with FDTD simulations and analyze the focal spot size to demonstrate its focusing capability.
language: en-US
businessId: focusing-with-slit
keywords: Finite Difference Time Domain(FDTD),Plasmonics
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Focusing_with_slit_cover.jpg
---

# Preface
Subwavelength optical devices hold great potential in light field manipulation and photonic integration. Compared with conventional optical elements, they can control light at scales much smaller than the wavelength, enabling higher integration density and multifunctionality. In particular, focusing-type subwavelength devices can enhance the directionality and concentration of light, achieving far-field focusing at the micro/nano scale. Such capabilities open new possibilities for high-resolution imaging, near-field probing, and efficient coupling in optical communication.

However, at subwavelength scales, light undergoes strong interference and diffraction, making it difficult to achieve efficient focusing. *Garcia-Vidal et al[^1]* proposed a structure consisting of a single subwavelength aperture in a metallic film surrounded by periodic surface grooves. By exciting surface plasmons, this design enables far-field focusing. In this case, we reproduce the structure with FDTD simulations and analyze the focal spot size to demonstrate its focusing capability.

![structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Focusing_with_slit_structure.png)

# Simulation settings
## Device introduction
As shown in the figure above, the structure consists of 20 grooves on the output surface with a period of $d=500\ nm$, depth $h=83.5\ nm$, and width $a=40\ nm$, which is also the width of the central subwavelength aperture. Since *Garcia-Vidal et al[^1]* assumed the metal to be a perfect conductor in their theoretical calculations, the structure is modeled using a Perfect Electric Conductor (PEC) in the FDTD.

A plane wave source with a wavelength range of $500\ nm - 600\ nm$ is incident from the left side of the structure. Considering the symmetry of the geometry and source, an `Anti-Symmetric` boundary condition is applied in the $X$ direction to reduce the simulation domain by half. All other boundaries are set as `PML`. While using `PML` on both sides of a plane wave source may introduce diffraction and edge effects that distort the wavefront, these effects are negligible at the aperture. This is because the aperture is located at the center of the simulation region, and the simulation width is much larger than the aperture. Moreover, distortions near the PML edges are reflected by the PEC film, preventing them from reaching the aperture and ensuring reliable results.

![simulation](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Focusing_with_slit_simulation.png?1)

# Simulation results

After the simulation, the *Focusing_with_slit.msf* script is executed to extract results.

The electric field intensity along the line at $x=0$ is plotted, as shown below. The results show that the transmitted field is focused in the far field, with the focal position located at approximately $z=44\ \mu m$, where the field intensity reaches about $0.0083$.

![E_focallength](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Focusing_with_slit_E_focallength.png)

The field distribution in the $ZX$ plane is illustrated. It clearly shows that the light transmitted through the aperture gradually converges and forms a high-intensity region near the focal point. For clearer visualization, the `colorbar max` should be set to the field intensity at the focal spot.

![E_ZX](    
https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Focusing_with_slit_E_ZX.png)

The field profile along the $x$ direction at the focal plane is shown below. The full width at half maximum (FWHM) of the focal spot is approximately $3.27\ \mu m$, confirming that this structure achieves far-field focusing beyond the diffraction limit. The results are consistent with the findings of *Garcia-Vidal et al[^1]*.

![E_focus](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Focusing_with_slit_E_focus.png)


# References
[^1]: F. J. Garcia-Vidal, L. Martin-Moreno, H. J. Lezec, and T. W. Ebbesen, “Focusing light with a single subwavelength aperture flanked by surface corrugations,” Appl. Phys. Lett. 83, 4500 (2003).