---
title: Metalens Based on PB Phase
description: Traditional curved optical lenses rely on phase accumulation along the light path to control light, which is limited by the refractive index of natural materials. To correct various image aberrations, multiple lenses are usually needed. However, combining multiple optical lenses occupies a lot of space, making it difficult to miniaturize optical systems. Metalenses, however, manipulate incident light to bend beams through the arrangement of artificial sub-wavelength units on the dielectric surface. A single metalens can achieve the same performance as a device that requires multiple optical lenses. Compared to traditional optical lenses, metalenses are smaller, lighter, cheaper, have better imaging quality, and are easier to integrate. They provide a new solution for compact integrated optical systems. This case study, based on the research of Xicheng Xia and Zan Yao, introduces how to use FDTD to simulate metalenses, helping readers achieve miniaturization of optical systems.
language: en-US
businessId: metalens-based-on-pb-phase
keywords: Finite Difference Time Domain,FDTD,Metalens,Phase control,PB phase
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_cover_new.jpg
---

# Preface

Traditional curved optical lenses rely on phase accumulation along the light path to control light, which is limited by the refractive index of natural materials. To correct various image aberrations, multiple lenses are usually needed. However, combining multiple optical lenses occupies a lot of space, making it difficult to miniaturize optical systems. Metalenses, however, manipulate incident light to bend beams through the arrangement of artificial sub-wavelength units on the dielectric surface. A single metalens can achieve the same performance as a device that requires multiple optical lenses. Compared to traditional optical lenses, metalenses are smaller, lighter, cheaper, have better imaging quality, and are easier to integrate. They provide a new solution for compact integrated optical systems. This case study, based on the research of _Xicheng Xia and Zan Yao[^1]_, introduces how to use FDTD to simulate metalenses, helping readers achieve miniaturization of optical systems.

![Metalens_PBPhase_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_structuer.png)

# Simulation settings

## Device construction

The structure of the metalens used in this case is shown in the figure above. The upper layer is glass, the lower layer is a gold film with a thick of 40 $nm$, and there is an aperture with a diameter of 10 $\mu m$ on the bottom surface of the gold film. There are many rectangular etched holes on the gold film. The length and width of each etched hole are $L$ = 215 $nm$ and $W$ = 60 $nm$, respectively. Each etched hole has a different rotation angle, introducing different phase shifts to the plane wave, ultimately modulating it into a spherical wave. To modulate the plane wave into a spherical wave, the required phase distribution on the surface of the metalens is:

$$\varphi_{r}=k_0(\sqrt{r^2+f^2}-f)$$

According to the PB phase theory, when circularly polarized light is incident normally, the transmitted cross-polarized light will carry an additional phase of $2\theta$, where $\theta$ is the rotation angle of the rectangular etched hole unit. Therefore, the required rotation angle of each etched hole on the metalens can be expressed using its coordinates relative to the lens center:

$$\theta_{x_i,y_i}=\frac{k_0}{2}(\sqrt{x_i^2+y_i^2+f^2}-f)$$

The _etch_ structure group of the project includes the scripts for constructing these etched holes. You only need to set the corresponding `Variables` in the structure group according to the design requirements.

![phase](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_phase.png)

Since the etched holes overlap with the gold film, the refractive index needs to be set to 1 when creating the etched hole structure, and the Mesh order should also be set to 1. For specific details, please refer to [Mesh order](/localhost/knowledge-base/User-Manual_mesh-setting?anchor=81).

## Source

Most metalenses are designed based on linearly polarized light. However, the PB phase used in this case refers to a geometric phase relationship for circularly polarized light discovered by _Pancharatnam and Berry_. When circularly polarized light is incident on the structure, it will generate cross-circularly polarized light with the opposite rotation direction to the incident light. Through appropriate structural design, the effect of rotating the optical axis can be achieved. By changing the angle between the optical axis and the coordinate axis, the phase of the cross-circularly polarized light can be controlled.

In this case, a plane light source is added below the structure, incident along the positive $Z$ axis. This software includes various polarization types for light sources, which can be conveniently selected in the `Polarization` tab of the light source properties window. Here, Left Circularly polarized light is chosen, as shown in the figure below.

![SourcePolarization](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_SourcePolarization.png)

# Simulation results

## Unit Cell

The attached _Unit_cell.mpps_ is a simulation project for a single period of the metalens. The project contains two parameter sweeps: _Phase_sweep_ and _PCR_sweep_. Where _Phase_sweep_ scans the rotation angle of the etched holes from $0~360 \degree$ to study the phase changes of the transmitted light field. _PCR_sweep_ scans the wavelength of the incident light from $0.5-1\ \mu m$ to study the polarization conversion rate(PCR) at different wavelengths of incidence.

After running the parameter sweep, the phase distribution of the right circularly polarized light can be obtained when the left-handed polarized light is incident, as shown in the figure below.

![PhaseSweep](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_PhaseSweep_new.png)

As shown in the figure, with the rotation of the etched holes, the phase of the right circularly polarized light exhibits clear periodic changes, which is consistent with the PB phase theory.

The variation of PCR with wavelength is shown in the figure below. The maximum PCR of 17.3% is reached at the wavelength of 0.86 $\mu m$, which is less than 1% different from the results in reference.

![PCRSweep](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_PCRSweep_vbeta3.4.8.png)

## Full Lens

The _FullLens.mpps_ in the attachment is a full lens simulation project. It is designed for a wavelength of 0.86 $\mu m$ with a focal length of $f$=4 $\mu m$. After simulation, you can obtain the electric field vector map near the focal point through the attached _FullLens.msf_ script. You need to click on the settings in the figure window and follow the settings below to obtain an image consistent with this article.

![Evector](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_Evector.png)

It can be seen that the light here is right circularly polarized, different from the incident left circularly polarized light, indicating that the metalens conforms to the PB phase theory. The propagation electric field intensity distribution after the light source passes through the lens is shown in the figure below. We can see that the light source successfully converges after passing through the metalens, with the focal point located at z=3.8 $\mu m$, differing by 5% from the designed focal length.

![E2_ZXPlane](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_E2_ZXPlane.png)

![E2_X0](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_E2_X0.png)

To verify whether the focused energy spot is consistent with the designed focal point, the full width at half maximum (FWHM) of the focal spot is used to characterize the quality of the spot focus. The theoretical calculation formula for FWHM is as follows:

$$FWHM=\frac{\lambda}{2NA}$$

In the formula, $\lambda$ is the design wavelength, numerical aperture $NA=nsin{\alpha}$, where $n$ is the refractive index of the medium, approximately 1 in air, and $\alpha$ is the aperture angle. Through theoretical calculations, the $FWHM_{theory}$ is found to be 595 $nm$.

The distribution of the electric field intensity at the focal point is shown in the following figure. The FWHM can be calculated as 596 $nm$, which is consistent with the theoretical value.

![Focus_XYPlane](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_E2_Focus_XYPlane.png)

![Focus_y0](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Metalens_PBPhase_E2_Focus_y0.png)

The script also calculates the focusing efficiency of the lens: within the focal plane, the ratio of the transmitted power inside a circle with the focal spot center as the origin and three times the FWHM as the diameter to the total power passing through the aperture is 39.6%. The simulation results verify the correctness of the theory and design.

# References

[^1]: Xicheng Xia, Zan Yao. Design of Plasma Metalens Based on PB Phase[J]. New technologies and new processes, 2020, (08): 46-48.
