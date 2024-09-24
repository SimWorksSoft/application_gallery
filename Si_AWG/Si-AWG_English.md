---
title: Si-Based Arrayed Waveguide Grating
description: Arrayed waveguide gratings (AWGs) are essential components in dense wavelength division multiplexed (DWDM) systems. As large-scale photonic integrated devices continue to evolve, the miniaturization design of AWGs has become an important topic. In this example, a 2.5D-FDTD solver in SimWorks Finite Difference Solutions was employed to simulate a saddle-shaped silicon nanowire AWG to investigate its output spectral response and loss.
language: en-US
businessId: si-based-arrayed-waveguide-grating
keywords: Finite Difference Time Domain(FDTD),Si-based Arrayed Waveguide Grating(AWG),Channel spacing,Free Spectral Range(FSR),Insertion loss
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/Si_AWG_Eout_20240304131830A017.jpg
---

# Preface

Arrayed waveguide gratings (AWGs) are essential components in dense wavelength division multiplexed (DWDM) systems. As large-scale photonic integrated devices continue to evolve, the miniaturization design of AWGs has become an important topic. Silicon nanowires, with their high contrast of refractive index between the core and cladding, allow light to be confined within smaller waveguides, which enables the smaller curvature radius with same bending loss and decreased spacing between arrayed waveguides under the same crosstalk. As a result, silicon-based AWGs become a good candidate technology to facilitate the (de)multiplexer integration.

In this example, a 2.5D-FDTD solver was employed to simulate a saddle-shaped silicon nanowire AWG to investigate its output spectral response and loss, as depicted in the figure. Due to the large structural dimensions of AWGs, 3D-FDTD simulations consume significant computational resources and cost long simulation time. In contrast, 2.5D-FDTD employs the equivalent materials since the structure remains same in the vertical direction, transforming the 3D problem into a 2D problem. Thus, the simulation can be greatly simplified while keeping similar simulation accuracy.

![Si_AWG_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Si_AWG_structure.png)

# Simulation settings

## Structure

In this example, the design of the Si-AWG is referenced from the publication[^1] and employs one input waveguide and three output waveguides. The design assumes three conditions: (1)Material parameters are taken from the TE fundamental mode at central wavelength at room temperature; (2)The diameter of the Roland circle is significantly larger than the core-to-core distance at the input/output couplers of AWGs; (3)The difference in effective refractive index and group refractive index between the curved waveguide and the straight waveguide can be neglected. The structure used in this example is illustrated in the figure below, with a working central wavelength $\lambda_{c}$ of $1.55 \mu m$ and a channel spacing $\Delta \lambda$ of $8 nm$.

![Si_AWG_structure_diagram](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Si_AWG_structure_diagram.png)

|                                                variables                                                |        symbol         |    value     |
| :-----------------------------------------------------------------------------------------------------: | :-------------------: | :----------: |
|                                           Free spectral width                                           | $\Delta\lambda_{FSR}$ |    $64nm$    |
|                                        Straight waveguide width                                         |          $w$          |  $0.5\mu m$  |
|                                       Number of arrayed waveguide                                       |         $N_a$         |     $25$     |
|                         Core-core distance of each input/output/array waveguide                         |    $d_{io}$, $d_a$    |  $1.5\mu m$  |
|     Width of the taper connecting the arrayed waveguide and planar waveguide at the grating circle      |        $w_t^a$        |  $1.5\mu m$  |
| Width of the taper connecting the input/output waveguides and the planar waveguide at the Roland circle |      $w_t^{io}$       |  $1.5\mu m$  |
|                                             Length of taper                                             |     $L_{taper}^a$     |  $10\mu m$   |
|                                    Length of input/output waveguide                                     |   $L_{taper}^{io}$    |   $5\mu m$   |
|                                       Radius of bending waveguide                                       |          $r$          |   $5\mu m$   |
|                    Length of the straight waveguide in the shortest array waveguide                     |         $L_1$         |   $0\mu m$   |
|                                        Diameter of Roland circle                                        |         $L_f$         | $33.27\mu m$ |
|                               Adjacent array waveguide length difference                                |         $dL$          | $11.77\mu m$ |

## Solver settings

For Si_AWG, the part of arrayed waveguide contains only waveguide structures that support stable transmission and generate phase delays in each channel. Consequently, the each part of arrayed waveguide grating can be simulated separately: the input planar waveguide and the output planar waveguide, as shown below. So the simulation region can be greatly reduced, leading to much shorter simulation time.

![SI_AWG_source](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Si_AWG_source.png)

## Source

Since we separate the AWG simulation into two parts, the light source for each arrayed waveguide in the output region must be guaranteed to be the same as the mode of each arrayed waveguide coupled by the light source through the input planar waveguide. From the above figure, we observe that the light is injected to the output tapered waveguide with a certain angle after passing through the arrayed waveguide. Therefore, we should align the injection direction of the mode sources with the middle axis angle of the tapered waveguides. Our mode solver will automatically calculate the propagation mode in the current direction.

We also need to set the amplitude of each mode source to match the transmittance of light coupled from the input waveguide into each individual waveguide in the array. And the pulse delays of each mode source should be computed based on the phase delays from length differences in arrayed waveguide. Thus, the pulse delay of the mode source can be calculated as follows:
$$\Delta(t)=\frac{dL n_g^a}{c}$$
where $dL$ is the length difference between neighboring array waveguides, $n_g^a$ is the group refractive index of the array waveguide, and $c$ is the speed of light in vacuum.

# Simulation results

## Input planar waveguide region

The `FDFP` monitor placed within the silicon substrate records the electric field distribution at a wavelength of $1.55\mu m$ as light propagates from the input waveguide into the arrayed waveguide. From the diagram below, we observe that light couples from the input waveguide to the input planar waveguide region, undergoes beam expansion, freely propagates to the edge of the Roland circle, and subsequently couples into the arrayed waveguide.

![Si_AWG_Ein](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Si_AWG_Ein.png)

The figure below shows the transmission rates within each of the 25 tapers placed at the top of the arrayed waveguide and oriented perpendicular to the waveguide, which indicates that most of the injected energy is effectively coupled into the arrayed waveguide.

![SI_AWG_T_forward](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SI_AWG_T_forward.png)

## Output planar waveguide region

The mode injected by the leftmost mode source as shown below. You can see that the mode source is still correct when it is angled.

![Si_AWG_mode](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Si_AWG_mode.png?)

The electric field distribution of light with a wavelength of $1.5465\mu m$, obtained from the `FDFP` monitor placed inside the silicon substrate, is depicted in the figure below. Multiple channels of light enter the arrayed waveguide, couple into the Roland circle, and undergo diffraction. Eventually, at the edge of the output waveguide, they converge into a strong beam, which couples into the output waveguide. Adjacent to the strongest diffracted light, there are two weaker diffraction beams corresponding to diffraction orders $m\pm1$.

![Si_AWG_Eout](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Si_AWG_Eout.png)

The transmission rate of three output waveguides as a function of wavelength is shown in the figure below. This AWG exhibits a channel spacing of $8.1nm$ and a free spectral width of $64.5nm$, which aligns with the design specifications.

![SI_AWG_T_backward](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SI_AWG_T_backward.png)

The figure below illustrates the loss of the three output waveguides as a function of wavelength obtained from the `FDFP` monitors. Notably, the device exhibits an insertion loss of $0.954146 dB$ and crosstalk levels below $-10 dB$.

![SI_AWG_loss](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SI_AWG_loss.png)

# References

[^1]: Huamao H. Research on arrayed waveguide gratings based on silicon nanowires[D]. Huazhong University of Science and Technology, 2010.
