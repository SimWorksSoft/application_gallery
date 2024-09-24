---
title: Y Branch
description: The power splitter based on Y branch distributes optical power to two or more output devices in a certain ratio. In this example, we use SimWorks Finite Difference Solutions to simulate the insertion loss, transmitted power and S-parameters of a symmetric 50/50 Y-branch splitter.
language: en-US
businessId: y-branch
keywords: Finite Difference Time Domain(FDTD),Y Branch,Insertion loss, S-parameters
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/YBranch_structure_20231214145344A237.jpg
---

# Preface

Y branch waveguide is a kind of important single component in integrated photonic devices, which has a wide range of applications, such as waveguide interferometer, modulator, optical switch, optical power splitter and so on. The power splitter based on Y branch distributes optical power to two or more output devices in a certain ratio. Structurally, Y-branch splitter can be divided into symmetric and asymmetric types. In this example, we use FDTD to simulate the insertion loss, transmitted power and S-parameters of a symmetric Y-branch splitter.
![YBranch_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/YBranch_structure.png)

# Simulation settings

The Y-branch splitter is placed inside the glass. The `Mesh Order` in the FDTD solver determines which material to use in the overlapped region, with larger values having higher priority. So in this example, the `Mesh Order` of Si is set to 1 and the `Mesh Order` of $SiO_{2}$ is set to 0.

In this example, the Y-branch splitter is symmetric up and down. The `force symmetric y mesh` function can be used to ensure that the mesh distribution of the top parts is same as that of bottom parts in the structure. The index_x distribution in the following figure demonstrates that the discretized structure constructed in the simulation is also symmetrical up and down, which satisfies our requirements.
![YBranch_index](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/YBranch_index_x.png)

# Simulation results

Since the device is symmetric from top to bottom, the light intensity in port2 and port3 should be equal when light is injected from port 1. The following figure shows the steady-state field distribution in the device, and the T curves of ports 2 and 3 obtained from the `Frequency-Domain Field and Power (FDFP)` monitor. As shown in the figure on the right below, the transmittances of the two output ports are almost equal (within 7.4E-08).
![YBranch_E](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/YBranch_E_154077.png)![YBranch_T](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/YBranch_Transmission_release1.3.0.png)

# Parameter Analyses

S-parameters are reflection and transmission coefficients of complex amplitude used to characterize the input/output relationship between the different ports of the device. The attached project contains a pre-defined S-parameter matrix sweep. Three ports with two modes have been added to the sweep. After running S-parameter sweep, the following figures indicate the normalized power transmission (abs^2 of s parameters) and insertion loss from port 1 to port 2 and port 3 in TE1 and TM0 modes.
![YBranch_SMatrixT](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/YBranch_SMatrix_T.png)![YBranch_SMatrixloss](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/YBranch_SMatrix_loss.png)
As shown in the first figure above, the transmittance of S21 is equal to the transmittance of S31 at the corresponding mode, which generates ~50-50 splitting ratio of the Y-branch splitter. In the second figure above, it can be seen that the insertion loss of the two ports at the TM0 mode is less than 4dB within the operating bandwidth, and the insertion loss of the TE1 mode is between 11-14dB. In conclusion, the Y splitter in this example has small insertion loss for the fundamental mode (TM0).
