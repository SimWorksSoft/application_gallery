---
title: Multi-Mode Interference (MMI) Coupler
description: The Multi-mode Interference (MMI) coupler is composed of three parts: input waveguide, output waveguide, and multimode interference region. When the optical field is injected into the multimode interference region through the input waveguide, the interference between multiple modes produces a self-imaging effect. This effect causes periodic generations of one or more images of the input field along the propagation direction of the guided wave. As a result, the MMI can achieve optical wavelength division multiplexing/demultiplexing, power division, polarizing splitter and other functions by this effect.
language: en-US
businessId: mmi-coupler
keywords: Finite Difference Time Domain(FDTD),Multi-Mode Interference Coupler,Optical waveguide
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/MMI_FDTD_port_mode_source_TE0_20231218111526A244.jpg
---

# Preface

The Multi-mode Interference (MMI) coupler is composed of three parts: input waveguide, output waveguide, and multimode interference region. When the optical field is injected into the multimode interference region through the input waveguide, the interference between multiple modes produces a self-imaging effect. This effect causes periodic generations of one or more images of the input field along the propagation direction of the guided wave. As a result, the MMI can achieve optical wavelength division multiplexing/demultiplexing, power division, polarizing splitter and other functions by this effect.

![design_without_taper](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/MMI_structures_design_without_taper.png)

- self-imaging effect
  The self-imaging effect is the theoretical basis of MMI. According to this theory, the length of the interference region of a 1xN symmetric MMI coupler is generally located at the position of the first N-fold image, which is calculated as follows:

$$L_{MMI}=\frac{3L_\pi}{4N}$$

where $L_\pi=\pi/(\beta_0-\beta_1)\approx 4n_rW^2/(3\lambda)$, $\beta_0$, $\beta_1$ are the propagation constants of the fundamental and first-order eigenmodes, respectively; $n_r$ is the refractive index of the waveguide, and $W$ is the width of the MMI waveguide. For details, please refer to Ref. 1[^1].

In this example, the taper waveguide is smoothly connected between the input/output waveguide and the MMI region. It significantly minimizes the impact of longitudinal multimode on imaging non-uniformity, and also reduces the loss due to reflection at the junction between the single-mode waveguide and the MMI region.

The performance of the device is affected by the geometric parameters of the waveguide, taper structure, and MMI region. It is difficult to determine the proper size of each part during the design process and even harder to assure the best solutions after integration just by using each optimal parameter of each part. This example utilizes Optimizations and Sweeps functions to analyze and optimize the parameters and models.

# Simulation settings

This example builds a MMI coupler with 1x2 ports in a 3D FDTD simulation. To make the device as compact as possible, the shortest length of MMI is set at the two-fold self-image. By using the calculation formula and reference [^2], we obtained the parameters shown below. The device is illustrated in the following figure.

![structures](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/MMI_structures_mpps.png)

|               Parameter                |     Symbol      |    Value    |
| :------------------------------------: | :-------------: | :---------: |
|             $MMI~~length$              |    $L_{MMI}$    |  $32\mu m$  |
|              $MMI~~width$              |    $W_{MMI}$    |  $6\mu m$   |
|             $MMI~~height$              |       $~$       | $0.22\mu m$ |
|            $Taper~~length$             |   $L_{taper}$   |  $10\mu m$  |
|             $Taper~~width$             |   $W_{taper}$   | $1.1\mu m$  |
|           $Waveguide~~width$           | $W_{waveguide}$ | $0.4\mu m$  |
| $Separations~~between~~output~~tapers$ |       $S$       | $3.14\mu m$ |

In this example, this MMI coupler is not sensitive to the polarization, e.g., TE and TM modes. Here, the TE0 mode is selected as the port source and shown in below figure.

![mode_source_TE0](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/MMI_FDTD_port_mode_source_TE0.png)

# Simulation results

Open the appendix project file and run it directly. The results of the `Frequency-Domain Field and Power` monitor clearly indicate that the energy of the incident beam is equally divided between the two output ports after the self-image effect in the MMI. In this case, the transmittivity of both output ports is equal.

![fdfp](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/MMI_FDFP_monitor_E.png)
![T_port2_and3](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/MMI_port2_and3_T_real.png)

# Parameter analyses

Following a successful simulation of a single project, Optimizations and Sweeps can be conducted to determine the impact of specific parameters on device performance, which enables the optimal device design.

## Optimization of MMI length

Using the theoretical value ($L_{MMI}$=33$\mu$m) as a reference, this example will utilize the Optimizations and Sweeps function to determine the best MMI length. The scanning range for the MMI length in this case is set to $29\mu m$~$34\mu m$. After running the `mmi_length` sweep in the appendix project, we observe that the transmittivity in port2 varies with the length of MMI. As shown in the figure, the optimal MMI length should be found between $31\mu m$ and $32\mu m$.

![mmi_length](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/MMI_lite_sweep_mmi_length_port2_T.png)

Based on the above sweep results, the MMI length can be further optimized by using the `optimization` function. The default algorithm used for Optimization is the Particle Swarm algorithm (see reference [^3]). Please note whether you choose to maximize or minimize the objective function, that is, select `Maximize` or `Minimize` in `Type`. The meaning of other parameters is referred to [Optimizations and Sweeps](/localhost/knowledge-base/User-Manual_optimization-and-sweep).

Set the optimization range for the MMI length from $31\mu m$ to $32\mu m$. Then, run the `mmi_length_optimization` in the project to obtain the results. Among the results, `best fom` represents the maximum transmittivity obtained, which is 0.475, `best parameters` represent the optimal MMI length obtained, which is $31.3\mu m$, and the meaning of other parameters is referred to [Optimizations and Sweeps](/localhost/knowledge-base/User-Manual_optimization-and-sweep).

## Optimization of Taper Width

For the width of the wedge structure, on the one hand, increasing its width can improve the quality of self-imaging and thus reduce the device loss; on the other hand, since the device is very compact and the spacing between the two output waveguides is very small, the width of the taper structure should be as small as possible to prevent the coupling crosstalk between the output waveguides. In this example, a parameter sweep was conducted on the taper width between $0.5\mu m$ and $1.5\mu m$ to select the optimal solution. Running the `taper_width` parameter sweep in the appendix yields the results shown in the below figure. After considering the spacing between the two output waveguides, the user can choose the appropriate width of the taper structure according to the desired transmittivity requirements.

![sweep_taper_width](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/lite_client_sweep_taper_width.png)

# References

[^1]: Soldano L B , Pennings E C M, "Optical multi-mode interference devices based on self-imaging: principles and applications," Journal of Lightwave Technology. 13(4):615-627 (1995)
[^2]: D. J. Thomson, Y. Hu, G. T. Reed and J. -M. Fedeli, "Low Loss MMI Couplers for High Performance MZI Modulators," in IEEE Photonics Technology Letters, 22(20),pp.1485-1487 (2010).
[^3]: J. Robinson and Y. Rahmat-Samii, "Particle swarm optimization in Electromagnetics," IEEE Trans. Antennas and Propagat. 52, pp.397 - 407 (2004).
