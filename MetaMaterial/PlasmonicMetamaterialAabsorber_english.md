---
title: Plasma Metamaterial Infrared Absorber
description: "Metamaterial" is a special type of man-made material with extraordinary physical properties that natural materials do not have, such as regulating the frequency, amplitude, phase, etc. of electromagnetic waves. This case models and simulates a Metal-Insulator-Metal (MIM) plasma metamaterial infrared absorber to study its reflection/transmission/absorption characteristics in the visible to near-infrared band.
language: en-US
businessId: plasma-metamaterial-infrared-absorber
keywords: Finite Difference Time Domain(FDTD),Metamaterial,Plasma metamaterial infrared absorber
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/InfraredAbsorber_structure_20240117162333A045.jpg
---

# Preface

"Metamaterial" is a special type of man-made material with extraordinary physical properties that natural materials do not have, such as regulating the frequency, amplitude, phase, etc. of electromagnetic waves. Metamaterials have a wide range of application prospects due to their exotic properties. For example, perfect absorbers designed based on metamaterials can be used as photodetectors, microbolometers, thermal imaging, etc. Based on the work of $Hao$ et al.[^1], this case models and simulates a Metal-Insulator-Metal (MIM) plasma metamaterial infrared absorber to study its reflection/transmission/absorption characteristics in the visible to near-infrared band.

# Simulation Setting

This case uses a MIM structure composed of silver-alumina-silver. The lower layer is an infinite flat plate of silver and aluminum oxide, and the upper layer is a periodic arrangement of silver cubes. The structure within one period is shown in the figure below. In optical simulation, we only need to simulate one cell. Due to the symmetry of the structure and plane wave source, we use `Anti-Symmetric` boundary conditions in the $X$ direction and `Symmetric` boundary conditions in the $Y$ direction. We can reduce the simulation space and thus the simulation time by using symmetric and anti-symmetric boundary conditions.

![InfraredAbsorber_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/InfraredAbsorber_structure.png)

| Parameters |     $W$     |     $t$     |     $d$      |     $h$     |     $a$     |
| :--------: | :---------: | :---------: | :----------: | :---------: | :---------: |
|    Size    | $0.05\mu m$ | $0.03\mu m$ | $0.012\mu m$ | $0.08\mu m$ | $0.25\mu m$ |

## Material

The metal used in this case is the Ag material created using the Drude model. For specific details about the Drude model, see [Debye, Drude, and Lorentz materials](/localhost/knowledge-base/User-Manual_debye-drude-lorentz-material):
$$\varepsilon_{total}(f) =\varepsilon+\frac{\omega_{p}^{2}}{-(2\pi f)^2+j2\pi f\gamma_{p}}$$

Among them, $\varepsilon=1$, plasma frequency $\omega_p=1.37 \times 10^{16}rad/s$, and collision frequency $\gamma_p=8.5 \times 10^{13}rad/s$. The real and imaginary parts of the permittivity of Ag calculated by the Drude model are shown below.

![InfraredAbsorber_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/InfraredAbsorber_fitting.png)

# Simulation Results

## Reflectivity, transmissivity and absorptivity

Based on the T data obtained from the `Frequency-Domain Field and Power(FDFP)` monitors at the top and bottom of the MIM infrared absorber, the reflectivity (R), transmissivity (T), and absorptivity (A) of the absorber are plotted, as shown in the figure below. It can be found that the peak absorptivity of the absorber at $0.59616\mu m$ is $0.99733$. The result is highly consistent with that shown in **Figure 2** in the reference.

![InfraredAbsorber_ART](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/InfraredAbsorber_ART.png)

## Electric field and resistive heat distribution

The figure below shows the electric field distribution of the MIM infrared absorber at a wavelength of $0.595\mu m$. It can be seen that an electric field enhancement effect occurs at the interface between the silver cube on the upper layer and the alumina. This is because the surface plasmon excitation resonance generated here traps the electric field in this small area.

![InfraredAbsorber_E](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/InfraredAbsorber_E.png)

The resistive heat formula is as follows:
$$Q=\pi c\varepsilon_{0}\varepsilon''(\lambda) |E(\lambda)|^{2}\lambda$$
Among them, $c$ is the speed of light, $\varepsilon_{0}$ is the vacuum permittivity, $\varepsilon''(\lambda)$ is the imaginary part of the permittivity, and $E$ is the electric intensity. The resistive heat distribution diagram of the MIM infrared absorber at a wavelength of $\lambda=0.595\mu m$ is as follows. It can be found that the resistive heat $Q$ is mostly limited at the edges and corners of the interface between the Ag cube on the upper layer and the alumina. The high absorptivity causes most of the energy at this wavelength to be converted into heat energy through loss.

![InfraredAbsorber_Q](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/InfraredAbsorber_Q.png)

# Reference

[^1]: Hao J, Zhou L, Qiu M. Nearly total absorption of light and heat generation by plasmonic metamaterials[J]. Physical Review B Condensed Matter, 2011, 83(16):5919-5926.
