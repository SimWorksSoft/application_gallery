---
title: Bandstructure of 2D Square Lattice
description: Photonic crystals, as a dielectric structure with periodic changes in dielectric constant, can prevent light of a specific frequency from propagating internally, forming a photonic band gap.
language: en-US
businessId: bandstructure-of-2d-square-lattice
keywords: Bandstructure,Square lattice,Photonic Crystal(PC),Finite Difference Time Domain(FDTD)
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/square-2D-online_20240108154638A002.jpg
---

# Preface

Photonic crystals, as a dielectric structure with periodic changes in dielectric constant, can prevent light of a specific frequency from propagating internally, forming a photonic band gap[^1]. In this case, a 2D square-lattice PC model is constructed and its bandstructure is analyzed using FDTD. Through this case, some special settings and precautions in FDTD simulations of PC bandstructure are introduced in detail.

![Graphica_Abstract.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Graphica_Abstract.png)

# Simulation settings

In this case, we use FDTD to analyze the bandstructure of a tetragonal photonic crystal composed of periodic arrangement of homogeneous dielectric cylinders. As shown in the figure, a uniform dielectric cylinder with a radius of $r$ is periodically arranged in air along the z and x axes with a lattice spacing of $a$ to form a 2D square-lattice photonic crystal. Since the 2D square-lattice structure changes periodically in the zx plane and the structural unit extends indefinitely in the y axis, in this case, the 2D FDTD solver is used for simulation and the simulation region is set to the 2D plane for calculation. For such periodic structures, periodic boundary conditions can be used in FDTD, and only one of the lattice units is required for this simulation, as shown in the dashed box in the figure below.

![square2D_lattice.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/square2D_lattice.png)

## Device construction

### Photonic crystal structure device

Different distributions of refractive index in photonic crystals generate different bandstructures, and the main factors determining the bandstructure of photonic crystals are the refractive index of the internal dielectric and the periodic constant of the structure [^2]. In this example, the refractive index of the dielectric material is 2.00, the background dielectric is air, the radius _r_ of the periodically arranged dielectric cylinder is 0.12 μm, and the lattice spacing _a_ of this square lattice is 0.5 μm. For the height of the cylinder, this parameter can be ignored in 2D FDTD and is set to 0.5 μm by default.
The built-in structure group library of the software contains some common photonic crystal structures. In this case, the **Rectangular lattice PC array** structure group can be directly selected to insert, and the corresponding script variables can be modified according to the device parameters.

![insert_rectangle_lattice.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/insert_rectangle_lattice_ribbon.png)

### Solver settings

#### Bloch boundary condition

In this case, the photonic crystal is formed by the dielectric cylinder arranged periodically in a square-lattice in 2D space, and the simulation can only be carried out on a periodic single lattice. To preserve the periodic array structure, Bloch periodic boundary conditions are used at the boundaries of the z and x axes of the simulation region. In the case of Bloch boundary conditions, you need to set the Bloch wave vector. At different wave vector $\vec{k}$, the modes that can exist stably in the photonic crystal are different[^3]. Bloch wave vectors are customized according to the Brillouin zone of the lattice. The user can check 'Using Source Angle', and the software will automatically set the Bloch wave vector according to the angle of the source. In this case, it is necessary to sweep the target wave vector, so the method of custom wave vector is adopted.

![simulation_BC_2d_square.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/simulation_BC_2d_square.png)

#### Forced mesh symmetry

For the photonic crystal simulation, it is necessary to ensure that the mesh generation method and mesh size of each structural unit are completely consistent, to ensure the unity and periodicity of the refractive index distribution, so as to avoid inaccurate calculation results. On the advanced settings page, you can check the 'force symmetric X/Z mesh' option in Mesh Generation to force the constructed mesh to be symmetric about the X/Z axis, which proves that the generated refractive index data fully conforms to the photonic crystal period conditions.

![fdtd-advanced-force-xz.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/fdtd-advanced-force-xz.png)

### Source and monitor

#### Analysis group：Dipole Clouds

For FDTD simulation, it is essential to incorporate a suitable light source as the input mode signal. To stimulate as many stable modes as possible within the photonic crystal, multiple broadband dipole sources with random orientations are randomly positioned within the simulation region. This Dipole array is constructed by adding 'Dipole Clouds', a software built-in analysis group. When constructing random Dipole sources using 'Dipole Clouds', values of script variable are set depending on the lattice type of photonic crystals to determine the distribution region and number of dipole sources. Different variables need to be set for different lattice types and simulation dimensions. (Introduction see [Analysis Group Setting](/localhost/knowledge-base/User-Manual_analysis-group-setting) page.)

![add-dipole.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/add-dipole_ribbon.png)

#### Analysis group：bandstructure

The built-in analysis group 'bandstructure' is added in the same way as the analysis group 'Dipole Clouds'. To calculate the spectrum under a specific wave vector, time monitors are used to collect the time signal of electromagnetic field excited by the dipole source array. By employing multiple time monitors with random locations in the target region, complete collection of mode signals can be ensured. In the 'Analysis-Script' of 'bandstructure' analysis group, Fourier transforms are performed on the time signals captured by each time monitor and then the desired Spectrum is generated by summarizing them. According to the principle of Fourier transform, in order to get more accurate results in the frequency domain, there must be long enough simulation time. Simultaneously, the interference mode signal existing at the beginning of the simulation should be fully attenuated, and finally the stable mode signal in the photonic crystal is obtained.

A 2D view of the device is shown below, as detailed in the attached file square2D.mpps. Next, simulation can be performed to obtain the target results and data post-processing can be performed.

![all-object](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/all-object.png)

# Simulation results

After the simulation is completed, the spectrum at a specific wave vector can be obtained by viewing the results of the analysis group. As shown in the figure below, when both Bloch wave vector components are zero, there are two resonance peaks in the spectrum, which indicates that two modes can stably exist in the photonic crystal under the Bloch wave vector.

![2dtm_spectrum_real.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/2dtm_spectrum_real.png)

For a 2D square-lattice, light waves propagate only in the zx plane, and the wave vector component ky outside the plane is equal to 0. The irreducible Brillouin zone is the triangle Γ-X-M as shown in the figure below. By adjusting the wave vector components kz and kx, the wave vector is obtained along the edge of the triangle, from the center Γ to X, then to M, and finally back to the center Γ. To calculate the bandstructure, it is necessary to obtain all modes that can exist stably under each target wave vector. Therefore, the spectrum under each wave vector is calculated by using parametric sweeps.

![GAMMA-X-M.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/GAMMA-X-M.png)

## Parameter analyses

In this case, it is imperative to conduct parameter sweeps for various Bloch wave vectors (bloch kz, bloch kx). The wave vectors in the bandstructure diagram are normalized wave vectors, which need to be converted to Bloch wave vectors in the FDTD solver. The range of the normalized wave vector can be determined by the special point coordinates of the Brillouin zone, and $k_{normalized}=k_{Bloch} * a/2/\pi$, so the corresponding Bloch wave vector range can be calculated from the normalized wave vector range. In this case, the spectrum under each wave vector is calculated to obtain a stable mode under each wave vector, so the result spectrum of the analysis group 'bandstructure' is selected as the output object of this parameter sweep.

After running the script, the software automatically displays the result, as shown in Figure 1 and Figure 2 below. Figure 1 is drawn from the wave vector, frequency and corresponding spectrum data. The horizontal axis in the figure represents the wave vector of Γ from the center of Brillouin zone to X, then to M, and finally back to the center. In the horizontal axis, 30 values of normalized wave vector are arranged based on the order of parameter sweeps. The vertical axis represents the frequency values. The colorbar color in the figure represents the signal amplitude of each frequency in the spectrum under each wave vector. The bandstructure of the photonic crystal can be seen from the color distribution in Figure 1. The final bandstructure diagram is shown in Figure 2, which is drawn from the wave vector and its corresponding normalized resonance frequency($f_{normalized}=f * a/c$) data. In the figure, the horizontal axis represents the normalized wave vector, the vertical axis represents the normalized frequency, and the points in the figure represent the mode that can exist stably under the corresponding wave vector.

![TM_figure1_2.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/TM_figure1_2.png)

The 2D photonic crystal is a periodic distribution of the dielectric in a plane, and when the light wave propagates in this plane, it can be regarded as two independent polarization modes, each polarization mode has its own bandstructure. In 2D FDTD, the bandstructure in TM and TE modes can be solved by changing the polarization type in the solver properties. Subsequently, the bandstructure of 2D square-lattice photonic crystals can be obtained according to the bandstructure diagram, where the band gap range corresponding to the TM/TE mode is shown as the shadow region in the figure below.

![TE-TM.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/TE-TM.png)

## References

[^1]: Joannopoulos J D , Villeneuve P R , Fan S . Photonic crystals: putting a new twist on light[J]. Nature, 1997, 386(6621):143-149.
[^2]: Joannopoulos J D , Johnson S G , Winn J N . Photonic crystals:molding the flow of light[M]. Princeton University Press, 1995.
[^3]: Kittel C . Introduction to Solid State Physics, 7th ed[M]. John Wiley & Sons, New York, 1996.
