---
title: Mode Source in Broadband Simulations
description: By default, mode source calculates mode at central frequency of the specified frequency range and then injects this mode at all frequencies, which is very effective in single-frequency and narrowband simulations. However, in broadband simulations, mode-mismatch errors increase as frequency range expands. In this example, the multi-frequency field of the mode source will be demonstrated using a copper wire with a thin dielectric coating operating in the broadband terahertz range.
language: en-US
businessId: mode-source-in-broadband
keywords: Finite Difference Time Domain(FDTD),Broadband simulation,Multi-frequency mode
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Broadband_modesource_cover.png
---

# Preface
By default, the mode source employs a frequency-domain algorithm to compute the mode fields that stably exist in the structure at the central frequency, and then injects that mode over all frequency ranges. This approach is highly effective for single-frequency and narrowband simulations. However, in broadband simulations, if the mode fields in the structure vary significantly for different frequencies, the error due to mode mismatch increases as the frequency range expands. Therefore, for broadband simulations, it is recommended to use multi-frequency field function to reduce mode mismatch errors.

As an example, let’s consider a copper wire with a thin dielectric coating operating in the broadband terahertz range. In this case, the injected mode exhibits dispersion due to the dielectric coating on the copper wire surface, leading to significant variations in mode profile with frequency. Multi-frequency mode sources are particularly advantageous in such broadband simulations, allowing for more accurate representation of mode behavior.

![Structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Broadband_modesource_structure.png)

# Simulation settings
## Device introduction
In this case, we use Perfect Electric Conductor (PEC) to simulate a copper wire with a radius of $0.5 mm$. Outside the copper wire, there is an additional dielectric coating with a thickness of $0.034 mm$ and a refractive index of $2.50998$. The mode source is incident vertically from the left side of the copper wire, as shown in the diagram above. Due to the structural and source symmetry, we can apply a `Symmetric` boundary condition in the $X_{min}$​ direction. Using symmetric boundary conditions allows us to reduce the simulation region by half, thereby saving memory resources.

## Source
In this case, the copper wire operates within a bandwidth of $0.9 THz$, and using the default mode source (single-frequency calculation) would result in significant errors due to mode mismatch at this broad frequency range. So we recommend enabling the `multi-frequency field` option for the mode source and setting the number of frequency points to 15. After solving, you can examine the distribution of mode field profiles as they vary with frequency, as shown in the following graph. Clearly, the mode field experiences substantial changes across frequencies in this simulation.

![Modefield](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Broadband_modesource_ModeField.png)

# Simulation results
Run the attached *Broadband_modesource_wire_multifreq.msf* script, which automatically sets up and runs a simulation project using the default mode source and a project using the multi-frequency mode source.

The injected pulse, the pulse propagated to the right side of the copper wire, and the back-scattering pulse are plotted over time when using the default mode source as follows:

![Ex_singlefreq](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Broadband_modesource_Ex_singlefreq.png)

It can be clearly seen that the mode of the center frequency does not match the mode of the whole frequency band, resulting in a large amount of back-scattering light. The injected pulse and back-scattering pulse interfere with each other and the signal is very unclear.


The following figure shows a plot of the injected pulse, the pulse propagated to the right side of the copper wire, and the back-scattering pulse when the multi-frequency field function is turned on.

![Ex_multifreq](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/Broadband_modesource_Ex_multifreq.png)

As can be seen from the figure, the injected pulse is very clear, with almost no backward scattering generated. The chirp signal due to dispersion as the injected pulse propagates along the copper wire to the right side is also very clean.