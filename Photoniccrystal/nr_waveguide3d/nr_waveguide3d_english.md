---
title: Bandstructure of a Magneto-Optical Waveguide
description: In this case, the optical waveguide model with periodic structure in the propagation axis is constructed, and the bandstructure of the waveguide is analyzed.
language: en-US
businessId: bandstructure-of-a-magneto-optical-waveguide
keywords: Bandstructure, Magneto-optical waveguide, Photonic Crystal(PC),Finite Difference Time Domain(FDTD), Periodic, Diagonal anisotropy,Isotropic,Anisotropic
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/nr_waveguide3d_20240108162224A006.jpg
---

# Preface

The FDE solver is used to solve modes for the waveguide whose structure is periodic in the propagation direction. However, for structures composed of anisotropic materials or other nonlinear materials, we can solve the dispersion or bandstructure by the FDTD solver. In this case, the optical waveguide model with periodic structure in the propagation axis is constructed, and the bandstructure of the waveguide composed of isotropic material and diagonal anisotropic material is analyzed respectively.

![nr_waveguide_3d.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nr_waveguide_3d.png)

# Simulation settings

## Device introduction

The FDTD solver is used in this case to analyze the bandstructure of an optical waveguide consisting of isotropic and anisotropic materials. Unlike the isotropic material, the dielectric constant of the anisotropic material is not equal in all directions, which will break the degeneracy between the modes and the calculated band structure will change significantly. The straight waveguide extends infinitely in the propagation axis, and its structure can be considered periodic. Therefore, periodic boundary conditions with only one cell in the simulation area are used in z-axis.

The refractive index of the isotropic waveguide core in this model is 1.5. As shown in the figure, the straight waveguide has a width $w$ of 2.6 μm and a height $h$ of 2 μm, extending infinitely along the z-axis. Dielectric materials with a refractive index of 1.4 were selected for the waveguide substrate.

![sectional_view_nrwave.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/sectional_view_nrwave.png)

## Device construction

Detailed information such as the object of the simulation model can be found in the attached project file nr_waveguide3d.mpps. In general, in order to calculate the complete bandstructure of the target structure, the dipole array is used as the input source that is set to the target frequency range. All the above-mentioned notices have been detailed in the bandstructure-related case. (See [Bandstructure of 2D Square Lattice](/localhost/case-detail/bandstructure-of-2d-square-lattice) for a detailed example of bandstructure simulation.) However, for this case, our goal is to find the influence of the waveguide material on the mode, and we only observe how the bandstructure changes with the adjustment of the waveguide system, so we use the mode source here instead of the dipole array. The mode source can solve the incident pattern, which converges more quickly. It can be found that the waveguide in this case supports two modes of TM and TE. Since these two modes are orthogonal, we construct two mode sources to inject two modes of TE and TM respectively, and solve these two modes in the wavelength range of 1.5 μm to 1.6 μm.

# Simulation results

The attachment nr_waveguide3d.mpps is the project file for this case. After downloading, the resonance spectrum under a specific wave vector can be obtained. Parameter sweeps were run to obtain the resonance spectrum at different wave vectors $k$. To speed up the operation, only five points are selected from the range $k_z = 5.6e ^{6}$~ $6.2e^{6} rad/m$. Running the parameter sweep can calculate the resonance spectrum at five different wave vectors. Once you're done, load and run the nr_waveguide3d.msf file to calculate the effective refractive index and propagation constant.

First, we simulate a regular waveguide composed of isotropic materials. The material of the waveguide core is set to a dielectric material with a refractive index of 1.5. After running the parameter sweep, open the nr_waveguide3d.msf file and run it. The effective refractive index can be calculated as $k/k_0$, where $k_0$ is the wave number in vacuum. The final figures such as effective refractive index vs wavelength, propagation constant vs wavelength are shown as follows:

![beta_neff_1.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/beta_neff_1.png)

The resonance spectrum at different wave vectors is shown below. Clearly, the mode degeneracy results in only one resonance peak per wave vector $k$ in an isotropic waveguide.

![sweep_spectrum.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/sweep_spectrum.png)

Next, the calculation of anisotropic material waveguides is performed. Click **Materials** in the main interface of the software to enter the **Material Library** window. Click "Go to Project Material Library" in the Material List to enter the project material library page. Double-click the material "core" to enter the editing interface of the material, check Anisotropy (Diagonal) here, and use diagonal anisotropic material. As shown in the figure, the refractive indices $xx$, $yy$ and $zz$ of the diagonal anisotropic material are entered into the corresponding input box as 1.49, 1.51 and 1.50, respectively.

![set_anisotropy_nr.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/set_anisotropy_nr.png)

Re-running the simulation, the spectrum of the anisotropic waveguide at a particular wave vector can be obtained. After running the parameter sweep again, run the attached script to view the calculation results of the anisotropic waveguide. As shown below, there are obvious differences in the effective refractive index and propagation constant corresponding to the two different modes.

![beta_neff_2.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/beta_neff_2.png)

The time monitor at the center of the waveguide records the variation of the electric field signal in the waveguide with time. The amplitudes of $E_x$ and $E_y$ are shown in the figure below. It can be seen that there is no coupling between the two modes, which is because the two modes are orthogonal to each other.

![Amplitude_Ex_Ey.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Amplitude_Ex_Ey.png)

As you can see in the figure below, instead of a single peak at each $k$ in the spectrum, there are now two resonance peaks. It indicates that there are two resonant frequencies corresponding to the two modes. This is due to the breaking of the degeneracy of TM and TE modes in the isotropic model.

![nr_waveguide3d_aniso_spectrum.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/nr_waveguide3d_aniso_spectrum.png)
