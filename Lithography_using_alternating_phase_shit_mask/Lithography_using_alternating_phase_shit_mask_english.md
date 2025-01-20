---
title: Lithography Using Alternating Phase Shift Mask
description: The demand for smaller, faster, and lower power semiconductor devices continuously drives advances in optical lithography technology. As the size of semiconductor devices continues to shrink, it is necessary to use alternating phase shift masks (APSM) to improve resolution. For example, at the 45nm node, some features to be imaged are smaller than the diffraction limit of the 193nm light source used. APSM modulates the phase so that the light interferes with itself after passing through the mask, making the mask pattern edges sharper and clearer, thereby improving pattern contrast. The proximity effects occurring at sub-wavelength scales need to be understood through lithography simulation, so they can be accounted for in mask design, ensuring a predictable and reliable process. This case demonstrates how to image sub-wavelength features using APSM in FDTD.
language: en-US
businessId: lithography-using-alternating-phase-shift-mask
keywords: Finite Difference Time Domain,FDTD,Lithography,Alternating Phase Shift Mask
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/APSM_cover.png
---

# Preface

The demand for smaller, faster, and lower power semiconductor devices continuously drives advances in optical lithography technology. As the size of semiconductor devices continues to shrink, it is necessary to use alternating phase shift masks (APSM) to improve resolution. For example, at the $45nm$ node, some features to be imaged are smaller than the diffraction limit of the $193nm$ light source used. APSM modulates the phase so that the light interferes with itself after passing through the mask, making the mask pattern edges sharper and clearer, thereby improving pattern contrast. The proximity effects occurring at sub-wavelength scales need to be understood through lithography simulation, so they can be accounted for in mask design, ensuring a predictable and reliable process. This case demonstrates how to image sub-wavelength features using APSM in FDTD.

![APSM_lithography_system](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/APSM_lithography_system.png)

# Simulation settings
## Device introduction

The structure of the APSM used in this case is shown in the figure below. The upper layer is a chrome APSM with checkerboard square windows, and the lower layer is a glass substrate. Each square window on the chrome APSM has a side length of $2\lambda=0.386\mu m$. The glass substrate is etched to a certain depth beneath the diagonally opposite windows, creating a $\pi$ phase difference between the light waves propagating through the alternately etched windows.

![APSM_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/APSM_structure.png)

The FDTD solver uses `Periodic` boundary conditions in the $X$ and $Y$ directions, and `PML` boundaries in the $Z$ direction. Using periodic boundaries allows simulation of an infinite array in those directions by simulating just one period. A plane wave with a wavelength of $\lambda=193nm$ is used to simulate the ArF excimer laser after passing through the illumination lens, with the polarization direction of the light source along the $X$ axis, as shown in the figure below.

![APSM_simulation](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/APSM_simulation.png)

# Simulation results

FDTD simulation strictly solves the near-field transmitted through the mask using the finite difference time domain algorithm. All refraction, diffraction, interference, absorption, and polarization effects are calculated in the near field of the mask, while the aerial image of the mask is obtained through post-processing of the FDTD simulation data.

## Near field distribution

After simulation, run the analysis script from the analysis group to plot the field intensity and phase of the near field at the upper surface of the chrome APSM, as shown in the figure below. It can be seen that the light intensity transmitted through each window varies significantly, and there is a $\pi$ phase difference between adjacent windows.

![APSM_Objectfield_intensity](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/APSM_Objectfield_intensity.png)

![APSM_Objectfield_phase](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/APSM_Objectfield_phase.png)

## Aerial image

The analysis script from the analysis group will also automatically post-process the near-field data to calculate the aerial image on the wafer when the numerical aperture (NA) of the projection system is $0.85$, as shown in the figure below.

![aerial_image_xpolarization](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/APSM_Objectfield_aerial_image_xpolarization.png)

To strictly calculate the aerial image on the wafer using FDTD, we assume that the light source and illumination optics use Kohler illumination. With Kohler illumination, points on the extended light source are assumed to be incoherent radiation. The optical system is arranged so that any point on the extended light source reaches the mask as a plane wave, with each point having a slightly different angle of incidence. Therefore, for a circular illumination aperture, one simulation must be performed for each orthogonal polarization state, and the results are summed according to intensity.

The attached project includes a pre-configured parameter sweep that can perform two simulations with light source polarization directions along the $X$ axis and $Y$ axis, respectively. After running the parameter sweep, the combined aerial image can be plotted using the attached *plot_incoherent.msf* script, as shown in the figure below.

![aerial_image](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/APSM_Objectfield_aerial_image.png)

Next, set the demagnification factor $M$ in the analysis group to 3, then rerun the parameter sweep and *plot_incoherent.msf* script. The following figure shows the aerial image on the wafer. It can be seen that with a demagnification factor $M=3$, the image remains very clear, and the background is clean.

![aerial_image_m3](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/APSM_Objectfield_aerial_image_M3.png)