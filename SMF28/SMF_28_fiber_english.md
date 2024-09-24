---
title: SMF-28 Fiber Mode Calculation
description: Single-mode fibers feature a smaller core diameter than multimode fibers, enabling the single-mode transmission within the operating wavelength range. This design improves the transmission performance and reliability of single-mode fibers. Single-mode fibers are widely used in communication fields, including long-distance fiber optic communication, data center interconnection, wireless base station backhaul, CATV, fiber optic sensing, etc. This case aims to demonstrate a simple mode calculation by taking SMF-28 single-mode fiber as an example.
language: en-US
businessId: smf-28-fiber-mode-calculation
keywords: Finite Difference Eigenmode(FDE),Single-mode fibers,Effective refractive index
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/SMF_28_structures_20240119151057A054.jpg
---

# Preface

Single-mode fibers feature a smaller core diameter than multimode fibers, enabling the single-mode transmission within the operating wavelength range. This design improves the transmission performance and reliability of single-mode fibers. Single-mode fibers are widely used in communication fields, including long-distance fiber optic communication, data center interconnection, wireless base station backhaul, CATV, fiber optic sensing, etc. This case aims to demonstrate a simple mode calculation by taking Corning® SMF-28 single-mode fiber as an example.

# Simulation Settings

In this case, the FDE 2D simulation method is used for mode solving purposes. The simulation structure is illustrated in the following figure, and the relevant parameters are listed in the following table. In the FDE simulation, symmetric/anti-symmetric boundary conditions are applied in the minimum x and z directions. These boundary conditions allow the simulation to ignore modes that do not satisfy symmetry requirements, allowing faster calculation of modes with specific symmetry. For details, see [boundary conditions](/localhost/knowledge-base/User-Manual_boundary-condition-settings).

![SMF_28_structures](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SMF_28_structures.png)

|   Denotation   | Dimension  | Refractive Index |
| :------------: | :--------: | :--------------: |
|   $r_{core}$   | 4.1$\mu m$ |       1.44       |
| $R_{cladding}$ | 50$\mu m$  |     1.434816     |

# Simulation Results

After opening the attachment project, setting the central wavelength to $1.55\mu m$ and executing `Model analysis`, the first mode solved is considered as the fundamental mode. The profile of this fundamental mode is shown in the figure below.

![TE0](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SMF_28_FDE_mode_solver_TE0.png)

The following describes the study on the transmission properties of SMF-28 optical fiber. For this purpose, disable symmetric/anti-symmetric boundary conditions, and set all boundaries as PEC. Then switch to `Frequency sweep analysis`, and set the wavelength range to $1.26\mu m$ ~ $1.66\mu m$ specifically for optical communication. After the simulation is completed, the trend of the effective refractive index of the fundamental mode as a function of wavelength is obtained, as shown in the figure below. For the fundamental mode, the effective refractive index is greater than the cladding refractive index over the entire wavelength range. As a result, the fundamental mode is effectively confined within the fiber core.

![neff](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SMF_28_FDE_analysis_neff.png)

In addition, the group velocity of optical pulses traveling in the fiber is also an extremely important parameter for signal delay/fidelity. According to the definition, the group refractive index is calculated as $n_g=c/v_g$. Based on the results, the curve of the group refractive index of the fundamental mode is plotted as a function of wavelength, as shown in the figure below.

![ng](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SMF_28_FDE_analysis_ng.png)

The above results reveal that the group velocity of the mode source varies at different frequencies, which leads to mode dispersion. The following mode dispersion curve is generated from the results. Obviously, the fundamental mode of SMF28 optical fiber exhibits a low dispersion coefficient across the entire operating frequency range, enabling the fiber to transmit signals over long distances while effectively avoiding signal distortion.

![mode_dispersion](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SMF_28_FDE_analysis_mode_dispersion.png)
