---
title: Organic Solar Cell with PC Structure
description: How to improve Organic solar cells'(OSCs) photoelectric conversion efficiency (PCE) is an urgent problem to be solved. One of the more commonly used methods is to add micro-nano structures for light trapping into the photoactive layer of OSCs to increase light absorption, thereby improving PCE. The photonic crystal (PC) structure is used in the photoactive layer of OSCs, which can enhance the light absorption of solar cells in specific wavelength bands. This case uses FDTD simulation to analyze the light absorption of an OSC with a 2D hexagonal-lattice PC structure.
language: en-US
businessId: organic-solar-cell-with-pc-structure
keywords: Finite Difference Time Domain(FDTD),Organic solar cell,Photonic Crystal(PC),Light absorption,Photoelectric conversion efficiency(PCE)
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/solar_organic_structure_20240117163819A047.jpg
---

# Preface

Organic solar cells (OSCs) have gradually become a research hotspot in the field of solar cells due to people's demand for clean energy and their advantages such as light weight, mechanical flexibility, and low manufacturing cost [^1]. How to improve its photoelectric conversion efficiency (PCE) is an urgent problem to be solved. One of the more commonly used methods is to add micro-nano structures for light trapping into the photoactive layer of OSCs to increase light absorption, thereby improving PCE. The photonic crystal (PC) structure is used in the photoactive layer of OSCs, which can enhance the light absorption of solar cells in specific wavelength bands. This case uses FDTD simulation to analyze the light absorption of an OSC with a 2D hexagonal-lattice PC structure.

![solar_organic_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_structure.png)

# Simulation settings

In the OSC used in this case, the photoactive layer is a bulk heterojunction mixture of _poly(3-hexylthiophene) (P3HT) and [6,6]--phenyl C61-butyric acid methylester (P3HT:PCBM) [^2][^3]_. The interior of the bulk heterojunction contains a PC structure formed by zinc oxide nanocrystals, which uses the leaky mode resonance between incident sunlight and the PC waveguide to improve the light absorption of solar cells in some wavelength bands [^4].

The structure and materials of the solar cell determine the PCE. Here, the OSC is a multi-layer cell structure containing PC nanostructures inside. For the PC material in this case, the refractive index of zinc oxide is 1.40, the radius r of the periodically arranged cylinders made of zinc oxide is 0.15 μm, the height is 0.12 μm, the lattice spacing of the hexagonal-lattice is 0.46 μm, and the thickness of the zinc oxide substrate is 0.07 μm. Above the zinc oxide PC substrate is a bulk heterojunction photoactive layer with a thickness of 0.193 μm. Above the structure is a layer of conductive polymer aqueous solution PEDOT:PSS, with a thickness of 0.05 μm. The surface of the solar cell is made of conductive glass (Indium tin oxide (ITO) coated glass) with a thickness of 0.178 μm, and the uppermost layer is covered by glass, with a refractive index of 1.52.

The device construction method in this case is similar to the silicon-based solar cell case ([Introduction link](/localhost/case-detail/planar-silicon-solar-cell)), which will not be repeated here. For details, download and read the attachment _OrganicSolarCellwithPC.mpps_ . The PC in this solar cell structure is a 2D hexagonal-lattice structure. See the special notes about 2D hexagonal-lattice band structure ([2D hexagonal-lattice band structure](/localhost/case-detail/bandstructure-of-2d-triangular-lattice)) for more relevant information.

## Material

To establish the material models of P3HT:PCBM, ITO, PEDOT:PSS and aluminum in the simulation, add a new 3D sampling data in the software and import the sampling data .txt file of the corresponding material in the attachment. The figure below shows the fitted curves for four materials in the solar spectrum range from 400nm to 700nm. These material data are extracted from references [^5][^6][^7].

![solar_organic_PSS_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_PSS_fitting.png)![solar_organic_PCBM_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_PCBM_fitting.png)

![solar_organic_ITO_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_ITO_fitting.png)![solar_organic_Al_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_Al_fitting.png)

# Simulation Results

Through the T data in the `FDFP` monitors on the top and bottom of the photoactive layer, the light absorption spectrum of the photoactive layer can be plotted as follows. It can be seen that the photoactive layer has a high absorptivity in the solar spectrum range, especially in the range of 400nm-600nm.

![solar_organic_Absorption](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_Absorption.png)

The absorption of the photoactive layer of the OSC without PC structure can be obtained through re-simulation after the hexagonal-lattice PC structure group in the attachment is disabled. The absorption curves of the photoactive layer with and without PC structures are plotted as follows:

![solar_organic_Absorption_without_PC](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/solar_organic_Absorption_without_PC.png)

As shown in the figure above, the absorptivity of the photoactive layer of the OSC with PC structures is slightly higher than that without PC structures at a wavelength of around 673nm. This enhancement is brought by the photonic bandgap of the PC itself, and its bandstructure can be further explored by the bandstructure analysis group.

# References

[^1]: Shi T , Zhang Z , Guo X , et al. Ultrafast Charge Generation Enhancement in Nanoscale Polymer Solar Cells with DIO Additive[J]. Nanomaterials, 2020, 10(11):2174.
[^2]: Tumbleston J R , Ko D H , Samulski E T , et al. Electrophotonic enhancement of bulk heterojunction organic solar cells through photonic crystal photoactive layer[J]. Applied Physics Letters, 2009, 94(3):25.
[^3]: Tumbleston J R , Ko D H , Samulski E T , et al. Absorption and quasiguided mode analysis of organic solar cells with photonic crystal photoactive layers[J]. Optics Express, 2009, 17(9):7670-7681.
[^4]: Ko D H , Tumbleston J R , Zhang L , et al. Photonic Crystal Geometry for Organic Solar Cells[J]. Nano Letters, 2009, 9(7):2742.
[^5]: Monestier F , Simon J J , Torchio P , et al. Modeling the short-circuit current density of polymer solar cells based on P3HT:PCBM blend[J]. Solar Energy Materials & Solar Cells, 2007, 91(5):405-410.
[^6]: Tumbleston J R , Ko D H , Lopez R , et al. Characterizing enhanced performance of nanopatterned bulk heterojunction organic photovoltaics[J]. International Society for Optics and Photonics, 2008.
[^7]: Palik, E. D. Handbook of optical constants of solids[M]. Academic press, 1998.
