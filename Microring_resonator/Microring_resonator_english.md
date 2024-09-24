---
title: Silicon Based Double Straight Waveguide Microring Resonator
description: In this case, the operation process and precautions are stressed by using FDTD solver to simulate microring resonance.
language: en-US
businessId: silicon-based-double-straight-waveguide-microring-resonator
keywords: Microring resonator,Resonant,Waveguide,Finite Difference Time Domain(FDTD),Silicon-On-Insulator(SOI)
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/ring_fdfp_data_e2_20240304131909A018.jpg
---

# Preface

In the silicon-based waveguide microring resonator, the special microring structure allows the light waves that meet the resonant conditions to interfere and superpose to generate resonance, which achieves the wavelength selection. Therefore, microring resonators are widely used in many fields. As shown in the figure, the typical waveguide-based resonator consists of two parallel straight waveguides and microrings between waveguides. In this case, the operation process and precautions are stressed by using FDTD solver to simulate microring resonance.

![orring3d.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/orring3d.png)

# Simulation settings

## Device introduction

The main parameters of the double-straight waveguide microring resonator are microring radius, waveguide spacing, waveguide width and waveguide height. In this device, a SOI structure with cross section size $0.4 \mu m×0.22 \mu m$ is used, where the width of the double straight waveguide, $wg_{width}$, is equal to the width of the microring waveguide, $ring_{width}$, and the waveguide spacing, $gap$, is $0.1 \mu m$. If the phase change is exactly equal to an integer multiple of $2 \pi$ when light propagates in a circle in the microring, that is, when the coherence condition is satisfied, all the light waves coupled into the microring will interfere with each other and produce a resonance enhancement effect.

$$2 \pi R n_{eff,wg} = m \lambda  $$

According to the above formula, the radius $R$ of the microring that satisfies the resonance requirement can be solved. When the central wavelength of the input source is $1.55 \mu m$, the effective refractive index of the optical mode can be solved by the mode solver. Thus, for the SOI structure with $0.4 \mu m×0.22 \mu m$ cross section, the theoretically calculated radius $R$ of the microring is about $2.9 \mu m$ when $m = 25$.

## Solver settings

The FDTD solver is used in this simulation. FDTD is used to calculate the time signals in the time domain, and the Fourier transform can be used to obtain the results in the frequency domain. For such high-Q devices as microring resonators, a longer simulation time is required in order to obtain more accurate simulation results, which is set to 5 ps here. To improve the simulation efficiency and maintain the calculation accuracy, the mesh type is set to the automatic non-uniform mesh, the accuracy level is set to 4, and the mesh refinement method is selected as the Conformal variant VP-EP. In addition, in order to solve mode of the port accurately, a uniform refined mesh is overridden between the coupling region of the waveguide and the ring.

Note: This software supports to build and edit simulation models through scripts. See [script function](/localhost/knowledge-base/Script-Commands_script-commands-overview) for more information. Attachments contain script files to complete the device building and simulation setup.

![ring_vpep_mesh.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/ring_vpep_mesh.png)

## Source

In this case, select "port" to input the mode source in the waveguide. For the double straight waveguide microring resonator, four corresponding ports are added to record the input and output data for further calculation of S-parameters, etc. Note: it is necessary to select a port as the source in the port group and set the source band, which is used to solve the injection mode and import the mode source.

![ring_port_1.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/ring_port_1.png)

# Simulation results

Once all the settings are complete, you can start running the simulation. The simulation control platform allows users to save the real-time transmission field, which is convenient for users to observe the resonance phenomenon, as shown in the following figure.

![ring_data_t.gif](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/transient_fields_ring.gif)

After the simulation, Mode Port and Monitor automatically save the observed information. The corresponding data visualization interface can obtain all result data. For more information, see [data visualization](/localhost/knowledge-base/User-Manual_data-visualizing) function introduction.

As shown in the below figure, T in the data list of each port shows the relationship between wavelength and transmission. Three resonance peaks around the $1.55 \mu m$ can be clearly seen.

![ring_fdfp_data_t.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/ring_fdfp_data_t4.png)

According to the resonance peak at the output port, the data of FDFP monitor ZX were viewed. The corresponding electric field magnitude at a wavelength of $1.55 \mu m$ is shown on the right of the following figure. It is clear that the field magnitude is significantly enhanced relative to the non-resonant wavelength of $1.54 \mu m$ (See left below).

![ring_fdfp_data_e.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/ring_fdfp_data_e2.png)

Note: After the simulation, this software supports viewing the results and post-processing data by scripts. The attachment contains the data visualization script for this case.

The analysis group "high Q analysis" that can analyze Q values of the three resonance peaks in the microring resonator has been added in the attachment project. After the simulation is completed, the Q values of the three resonance peaks can be obtained, and the results are shown as follows.

```msf
val =
Resonance 1:
val =
    frequency = 196.995THz, or 1521.83 nm
val =
    Q = 3608.12
val =
Resonance 2:
val =
    frequency = 189.921THz, or 1578.51 nm
val =
    Q = 1994.18
val =
Resonance 3:
val =
    frequency = 193.43THz, or 1549.88 nm
val =
    Q = 2672.63
```

# References

[1] Mirza, Asif , et al. "Silicon Photonic Microring Resonators: Design Optimization Under Fabrication Non-Uniformity." Design, Automation and Test in Europe Conference and Exhibition 2020.
[2] Zhou Z P. Silicon based optoelectronics. Peking University Press, 2012.
[3] Hammer, Manfred , K. R. Hiremath , and R. Stoffer . "Analytical Approaches to the Description of Optical Microresonator Devices." Aip Conference Proceedings (2004).
