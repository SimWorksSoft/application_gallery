---
title: Bragg Microcavity
description: Optical microcavities based on optical waveguides typically have a high quality factor and can be applied in various fields such as optical filters, lasers, and modulators. This case aims to analyze the resonance spectrum of a 1D Bragg grating microcavity based on an optical waveguide. Using the FDTD method, the resonant frequencies and quality factor Q are calculated too. By increasing the dimensions of the central structure of the Bragg grating, a defect is introduced that enables the occurrence of transmission resonance within the stopband of the Bragg structure.
language: en-US
businessId: bragg-microcavity
keywords: Finite Difference Time Domain(FDTD),Optical waveguide,Microcavity,Resonator
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/waveguide_bragg_microcavity_structures_20240119153335A056.jpg
---

# Preface

Optical microcavities based on optical waveguides typically have a high quality factor and can be applied in various fields such as optical filters, lasers, and modulators. This case aims to analyze the resonance spectrum of a 1D Bragg grating microcavity based on an optical waveguide. Using the FDTD method, the resonant frequencies and quality factor Q are calculated too. In the device shown below, the Bragg grating consists of a periodic toothed structure and six parallel air gaps distributed in the center of the structure. By increasing the dimensions of the central structure, a defect is introduced that enables the occurrence of transmission resonance within the stopband of the Bragg structure.

![structures](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/waveguide_bragg_microcavity_structures.png)

# Simulation Settings

In this case, a typical Bragg microcavity based on a waveguide structure is created in the 3D FDTD, with its structure shown in the figure below. To introduce a defect, the dimensions of the grating are set to be non-uniform. For details, see Reference [^1].

![simulati_structures](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/waveguide_bragg_microcavity_simulati_structures.png)

The use of the `Mode Source` requires selecting the optical mode to be injected into the waveguide. In this case, the fundamental mode with TE polarization is selected to excite the resonant microcavity. The mode profile is shown in the figure below. Multiple `FDFP monitor` are placed in the simulation region at different directions and positions to observe the field distribution. The built-in `high Q` analysis group is selected from the Analysis group library to solve for the resonant frequencies within the target frequency range and calculate the corresponding quality factor Q.

![TE0](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/waveguide_bragg_microcavity_modesource_TE0.png)

# Simulation Results

After opening the attached project and completing the run, all target analysis data can be retrieved from the monitors and analysis group. By running the attached script file `Waveguide_Bragg_Microcavity_analysis.msf`, the following figure is obtained. Clearly, the signal strength (Ex) obtained from the results of `Time Monitor out` reveals that most of the optical energy has already been radiated out within a time frame of approximately 1 ps. However, in order to ensure accurate calculation for the quality factor Q, it is necessary to obtain complete signal data within 2 ps.

![simulation_time](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/waveguide_bragg_microcavity_simulation_time.png)

After applying the Fast Fourier transform (FFT) to the time-domain signals, the resonance spectrum is obtained, as shown in the figure below. It can clearly be observed that the Bragg microcavity features a wide stopband and multiple resonant peaks are present within the target frequency range.

![fft_Ex](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/waveguide_bragg_microcavity_fft_Ex.png)

As shown in the following transmission spectrum, the resonant frequency is 196.8 THz. The corresponding quality factor Q, that is, the ratio of the center frequency to the full width at half maximum (FWHM) of the resonance peak, is determined by the `high Q` analysis group, which is approximately 199. The quality factor of a microcavity represents the ratio between energy stored and energy lost. Therefore, to achieve a higher Q factor, it is essential to minimize radiation losses.

![Q_factor](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/waveguide_bragg_microcavity_Q_factor.png)

The results of the FDFP monitors placed at the horizontal and vertical cross-sections of the microcavity structure reveal the field intensity distribution at different frequencies. The field intensity distributions at resonant and non-resonant frequencies are compared as shown in the following two figures. The first figure shows an approximately 6-fold enhancement in the resonant electric field at the Bragg microcavity. However, the second figure demonstrates that, under non-resonance conditions, a significant portion of the radiation is reflected by the Bragg microcavity structure.

![on_resonance](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/waveguide_bragg_microcavity_on_resonance.png)
![off_resonance](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/waveguide_bragg_microcavity_off_resonance.png)

# References

[^1]: Kleckner, T. C , Modotto, et al. "Design, Fabrication, and Characterization of Deep-Etched Waveguide Gratings", Lightwave Technology, Journal of, 2005, 23(11):3832-3842.
