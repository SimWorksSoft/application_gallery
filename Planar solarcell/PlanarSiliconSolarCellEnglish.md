---
title: Planar Silicon Solar Cell
description: Solar cell is a device that converts solar energy into electricity. When sunlight irradiates a semiconductor material with photovoltaic effect, electron-hole pairs (photogenerated carriers) are generated. An electric current can be produced by inducing electrodes at both ends of the solar cell. In this example, we simulate a planar silicon solar cell by SimWorks Finite Difference Solutions to calculate the absorption of solar energy (300-1100nm) and further to compute the photon generation rate and the corresponding photocurrent.
language: en-US
businessId: planar-silicon-solar-cell
keywords: Finite Difference Time Domain(FDTD),Solar cell,Generation rate
coverImg: https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/jpg/PlanarSolarCells_structure_20231214145049A236.jpg
---

# Preface

Solar energy is a clean and renewable energy. Therefore, the photovoltaic application of solar energy has become one of the most dynamic research fields in recent years. Solar cell is a device that converts solar energy into electricity. When sunlight irradiates a semiconductor material with photovoltaic effect, electron-hole pairs (photogenerated carriers) are generated. An electric current can be produced by inducing electrodes at both ends of the solar cell. In this example, we simulate a planar silicon solar cell by FDTD to calculate the absorption of solar energy ($300-1100nm$) and further to compute the photon generation rate and the corresponding photocurrent.

# Simulation Settings

This example uses a plane wave to simulate sunlight irradiation of a planar silicon solar cell. `Periodic` boundary conditions are used in the Z-direction to obtain simulation results for infinity periods in that direction using only one period.
![PlanarSolarCells_structure](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/PlanarSolarCells_structure.png)

## Material

The absorption of the device can be greatly affected by the Si and Al materials. Therefore, before simulation, it is necessary to check the fitting error between the model fitted and the data points (sampled data) in the simulation band. If the fitting error is lower than the default value (RMSE=0.1), the fitted model satisfies the simulation requirements. Otherwise, please adjust the target error and the coefficient to re-fit it. The following figure shows the results automatically fitted by the software that meet the tolerance requirements.
![PlanarSolarCell_si_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/PlanarSolarCell_si_fitting.png)![PlanarSolarCell_Al_fitting](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/PlanarSolarCell_Al_fitting.png)

# Simulation results

## Transmission and Absorption

The transmittance, absorptance, and reflectance can be plotted based on the T data obtained from the `FDFP` monitors at the top and bottom of the planar silicon solar cell. The figure shows that the transmittance of the entire cell is zero due to total reflection from the Al electrodes. The ripples in the reflectance are due to the Fabry-Perot effect.
![SolarCells_RT](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SolarCells_RT.png)

## Generation rate and Short-circuit current

The number of photons absorbed per unit volume is calculated by dividing the absorbed light energy by the energy per photon. Then the number of absorbed photons is integrated over the frequency as in the following equation to obtain the generation rate at different locations in the solar cell.
$$ G=\int\frac{-0.5 \omega|\vec{E}(\omega)|^2\cdot{imag[\varepsilon(\omega)]}}{\omega\hbar}d\omega $$
where $\varepsilon$ is the dielectric constant.
Assuming that each absorbed photon excites an electron-hole pair, a photocurrent can be generated. The formula for the current is:
$$I=eG$$
The equation above calculates the short-circuit current by using the generation rate. The total short-circuit current of the solar cell can be found by integrating the current. The current density of the short-circuit current of the solar cell is calculated to be approximately $242.641 A/m^2$. As there is no change in the Z direction in this case, we can just observe the change of the photon generation rate along the X axis (refer to the below figure).  
![SolarCells_GR](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SolarCells_GR.png)

## Optimization of absorption efficiency (reduction of reflections)

To address the issue of sunlight reflection off the solar cell during device operation, a $Si_3N_4$ (n=2.05) layer with 0.07$\mu$m is chosen as an anti-reflective layer (AR) to cover the surface of the solar cell. The AR structure should be changed to 'Enable' state in the software and re-run the simulation.
![SolarCells_RT_with_AR](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SolarCells_RT_with_AR.png)![SolarCells_GR_with_AR](https://simworksofficial-files.oss-cn-beijing.aliyuncs.com/mdfile/resources/img/SolarCells_GR_with_AR.png)
The first figure above shows the absorption rate calculated from the simulation data, and the second figure shows the generation rate in the X-direction. The calculated photocurrent is approximately $341.962 A/m^2$, indicating a significant increase after the addition of the anti-reflective layer.

# Appendixes

To calculate the generation rate, since the power of the plane wave used in the simulation is different from the power of sunlight, the generation rate must be normalized to the generation rate under sunlight. The provided `Solar.mat` Matlab data file contains the solar power spectrum in units of Watts per square meter per meter. These data are based on the values of `ASTM G-173-03`, which can be found at the following link [_National Renewable Energy Laboratory (NREL)_](https://www.nrel.gov/grid/solar-resource/spectra.html)
