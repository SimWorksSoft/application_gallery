---
title: Bandstructure of 3D Cubic Lattice
description: 3D Cubic Lattice is a special case of 3D Rectangular Lattice. The lattice spacing of this type of photonic crystal is equal in three axes in space.
language: en-US
businessId: bandstructure-of-3d-cubic-lattice
keywords: Bandstructure,Cubic lattice,Photonic Crystal(PC),Finite Difference Time Domain(FDTD)
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/3D_cubic-online_20240108155920A004.jpg
---

# Preface

3D Cubic Lattice is a special case of 3D Rectangular Lattice. The lattice spacing of this type of photonic crystal is equal in three axes in space. In this case, the 3D cubic-lattice photonic crystal is constructed, and the FDTD solver is used to simulate the bandstructure of the dielectric sphere 3D cubic-lattice photonic crystal.

![cubic_lattice.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/cubic_lattice.png)

# Simulation settings

## Device introduction

The FDTD solver is used to analyze the bandstructure of a cubic-lattice photonic crystal consisting of a periodic arrangement of spheres in a homogeneous medium. Similar to the 2D square-lattice photonic crystal, the periodic arrangement of the dielectric spheres in air realizes a periodically varying refractive index distribution in space, forming a photonic bandgap. In this example, the radius $R$ of the periodically arranged dielectric sphere is 0.13 μm, the refractive index of the dielectric material is 3.00, the background is air, and the lattice spacing $a$ of the cubic lattice is 0.5 μm.

## Device construction

The simulation settings of this case are similar to the [Bandstructure of 2D Square Lattice](/localhost/case-detail/bandstructure-of-2d-square-lattice) case. The attachment 3D_cubic.mpps is the demonstration file. After opening the project file, you can see the detailed parameters and settings. The 3D cubic lattice structure changes periodically in space in all three axes, which requires the use of 3D FDTD simulation. By adjusting the coordinates of the geometric center and the axial range of the FDTD, the simulation area is set to be the same as the periodic unit of the 3D cubic lattice, and the structural unit is located in the center of the simulation area, as shown in the following figure. In order to make the structural unit exhibit periodic distribution, Bloch boundary conditions are used along z, x and y axes. The analysis group 'Dipole Clouds' and 'bandstructure' are used to create a fixed number of dipole sources and time monitors at random locations in the 3D FDTD simulation region. Note that the variable of lattice type is changed to 3(3D rectangular lattice) in the analysis group 'Dipole Clouds'.

![all_object_cubic.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/all_object_cubic.png)

# Simulation results

Download and open the attachment 3D_cubic.mpps and run all parameter sweeps manually. After completing the parameter sweep of the wave vector, download the script file 3D_cubic.msf for calculating the corresponding bandstructure and run it to obtain the bandstructure diagram, as shown in the figure below. The bandgap range of the photonic crystal is shown as the shaded area in the figure.

![bandstructure_3D_cubic.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/bandstructure_3D_cubic.png)
