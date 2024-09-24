---
title: Bandstructure of BCC Lattice and FCC Lattice
description: In this case, BCC and FCC photonic crystals are constructed and their bandstructures are analyzed using FDTD solvers.
language: en-US
businessId: bandstructure-of-bcc-lattice-and-fcc-lattice
keywords: Body-Center Cubic(BCC) Lattice,Face-Center Cubic(FCC) Lattice,Bandstructure,Photonic Crystal(PC),Finite Difference Time Domain(FDTD)
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/BCC-FCC-online_20240108161207A005.jpg
---

# Preface

Body-Center Cubic Lattice (BCC) and Face-Center Cubic Lattice (FCC) are two common types of 3D photonic crystal structures. In this case, BCC and FCC photonic crystals are constructed and their bandstructures are analyzed using FDTD solvers.

![BCC_FCC.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/BCC_FCC.png)

# Simulation settings

## Device introduction

In this case, the FDTD solver is used to analyze the bandstructure of a photonic crystal composed of homogeneous dielectric spheres arranged according to two lattice structures, FCC and BCC. These two kinds of lattice structures belong to the cubic crystal system, but their minimum periodic structural elements are not rectangular structures, so they do not conform to the FDTD rectangular mesh algorithm. Therefore, different from the simulation settings of [Bandstructure of 3D Cubic Lattice](/localhost/case-detail/bandstructure-of-3d-cubic-lattice), special settings should be made for the simulation object based on the lattice type.

## Device construction

The construction and simulation Settings of the photonic crystal in this case are similar to the case [Bandstructure of 2D Square Lattice](/localhost/case-detail/bandstructure-of-2d-square-lattice), which will not be repeated here. Please download the attached project file to view the detailed information of the case. Both BCC and FCC lattices belong to the cubic crystal system, and their unit cell shapes are cubic, which meets the basic requirements of the FDTD solver for the rectangular simulation region. Therefore, the simulation region is set to be consistent with the space range of the simplest unit cell structure, and the region boundary is set to the Bloch periodic boundary condition. The primitive cell structure in the BCC and FCC lattices is shown in the figure below. Similar to the triangular lattice, it is obvious that its minimal periodic structure is non-rectangular. There are multiple primitive cell structures in the simulation region, and at least four primitive cell units in the simulation region of FCC lattice photonic crystal. Likewise, to avoid the problem of artificial region folding, add matching dipole sources in each primitive cell, see case [Bandstructure of 2D Triangular Lattice](/localhost/case-detail/bandstructure-of-2d-triangular-lattice) for more information. In addition, when generating the mesh in the FCC lattice simulation area, it is necessary to ensure that the mesh cells are uniformly and symmetricly distributed about the central coordinate axis, and the number of mesh cells in each axis can be divisible by 4. Thus, the meshes of each sphere structure are same, and the periodicity of the index distribution in the simulation region is realized. See the corresponding simulation in the attachment for details.

![bcc_fcc_p_u.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/bcc_fcc_p_u.png)

# Simulation results

Attachments contain project files for BCC- and FCC- lattice photonic crystal. Download and open the project files respectively. After running all the parameter sweeps, run the corresponding scripts to obtain the parameter sweep results and draw the bandstructure diagram, as shown in the following figure.

![bcc_bandstructure.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/bcc_bandstructure.png)

![fcc_bandstructure.png](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/fcc_bandstructure.png)
