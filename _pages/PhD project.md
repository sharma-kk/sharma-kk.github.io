---
layout: page
permalink: /phd-project/
title: PhD project
description: A brief look at the work I did during my PhD.
nav: true
nav_order: 2
---

Processes occurring in the Earth's atmosphere and ocean exhibit a wide range of spatial (a few millimeters to thousand of kilometers) and temporal (a few seconds to several decades) scales. In both media, small-scale motions coexist and interact with large-scale circulation.  Due to limited computational resources, however, it is practically impossible to capture all the scales in numerical simulations. The small scales which are not captured by the numerical models lead to errors in the prediction. Parameterization techniques are generally used to account for the missing effect of small scales on large scales. In our project, we explored the use of a parameterization technique known as `stochastic advection by Lie transport` (SALT).

In the literature, SALT has been successfully applied to numerous geophysical fluid dynamics (GFD) equations such as the 2D Euler equation, two-layer quasi-geostrophic model, and shallow water equation. In our project, we investigated SALT's efficacy in modeling the effect of unresolved scales on the resolved scales and quantifying the uncertainty due to unresolved scales for a `coupled ocean atmosphere climate model`. 

Our results demonstrate that ensemble forecasts from the stochastic climate model exhibit good reliability. Comparisons between the stochastic and deterministic model forecasts, reveal that the stochastic approach consistently outperforms the deterministic one throughout the simulation period.

The `stochastic climate model equations` are:

$$
\begin{align*}
\text{Atmosphere}: \ &\mathrm{d} \mathbf{u}^a + ((\mathbf{u}^a \mathrm{d} t + \textcolor{green}{\sum_i \boldsymbol{\xi}_i \circ \mathrm{d} W^i})\cdot \nabla) \mathbf{u}^a + \frac{1}{Ro^a} \hat{\mathbf{z}} \times (\mathbf{u}^a\mathrm{d} t + \textcolor{green}{\sum_i \boldsymbol{\xi}_i \circ \mathrm{d} W^i}) \\
                &\quad + \textcolor{green}{\sum_i (\sum_{j=1}^2 u_j^a \nabla \xi_{i,j} + \frac{1}{Ro^a}\nabla(\boldsymbol{\xi}_i \cdot \mathbf{R}))\circ \mathrm{d} W^i} = (-\frac{1}{C^a} \nabla \theta + \frac{1}{Re^a} \Delta \mathbf{u}^a) \mathrm{d} t, \\
        &\mathrm{d} \theta^a + \nabla\cdot(\theta^a (\mathbf{u}^a\mathrm{d} t + \textcolor{green}{\sum_i \boldsymbol{\xi}_i \circ \mathrm{d} W^i})) = ({\gamma(\theta^a - \theta^o)} + \frac{1}{Pe^a} \Delta \theta^a )\mathrm{d} t,\\
\text{Ocean}: \ &\frac{\partial \mathbf{u}^o}{\partial t} + (\mathbf{u}^o\cdot \nabla)\mathbf{u}^o + \frac{1}{Ro^o} \hat{\mathbf{z}} \times \mathbf{u}^o + \frac{1}{Ro^o} \nabla p^a = {\sigma(\mathbf{u}^o - \mathbb{E}\mathbf{u}_{sol}^a)} + \frac{1}{Re^o} \Delta \mathbf{u}^o,\\
    & \nabla \cdot \mathbf{u}^o = 0,\\
    &\frac{\partial \theta^o}{\partial t} + \mathbf{u}^o \cdot \nabla \theta^o = \frac{1}{Pe^o} \Delta \theta^o,
\end{align*}
$$

where the vector variable $\mathbf{u}$ and the scale variables $\theta$ and $p$ (with superscripts for the atmosphere and ocean components) denote the velocity, potential temperature, and pressure fields, respectively. The atmospheric temperature is coupled to the ocean temperature through the term $\gamma (\theta^a - \theta^o)$ representing the transfer of heat from the ocean to the atmosphere. The atmosphere and ocean velocities are coupled through the term $\sigma (\mathbf{u}^o - \mathbf{u}^a_{sol})$ which models the shear stress exerted by atmospheric winds on the ocean surface. 

Stochastic terms (shown in green) which model the small-scales can be estimated using the satellite data. In our work, we estimate the stochastic terms (mainly $\boldsymbol{\xi}_i$) using statistical analysis of velocity data obtained from high-resolution simulation of the deterministic model. 

### Key simulations


#### 1. An idealized deterministic atmosphere model

<img src="/assets/img/atmo_dom.png" alt="Schematic representation of the 2D domain for the atmosphere model" width="600"/>

*Figure 1: Schematic representation of the 2D domain on which the atmosphere model is simulated. The domain is an approximation of a section in the Earth's northern hemisphere (shown in left).*

`Model equations:`

$$
\begin{align*}\label{eq: final det atm model}
        &\frac{\partial \mathbf{u}}{\partial t} + (\mathbf{u}\cdot \nabla)\mathbf{u} + \frac{\hat{\mathbf{z}} \times \mathbf{u}}{Ro} + \frac{\nabla \theta}{C} = \nu_e \Delta \mathbf{u}, \\
        &\frac{\partial \theta}{\partial t} + \nabla\cdot(\theta \mathbf{u}) = \eta_e \Delta \theta.
\end{align*}
$$

`Discretization:` We used the Finite Element Method for spatial discretization and Crank-Nicolson scheme for temporal discretization. The model resolution i.e. the size of the small element size is $\sim 15$ km. The numerical implementation is carried out using Firedrake (an open source Python Finite Element Method package) and the visualization is done using Paraview. 

`Simulation results:`
<video width="600" controls title="Evolution of vorticity in the high-resolution deterministic atmosphere model">
  <source src="/assets/video/high_res_vort_t27_to_t45.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
*Video 1: Evolution of vorticity in the high-resolution deterministic atmosphere model.*


#### 2. Deterministic climate model equations

<img src="/assets/img/clim_mod_dom.png" alt="Schematic representation of the 2D domain for the climate model" width="600"/>

*Figure 1: Schematic representation of the 2D non-dimensionalized domain (right) used for the climate model simulations.*

`Model equations:`

$$
\begin{align*}
       \text{Atmosphere}: \ &\frac{\partial \mathbf{u}^a}{\partial t} + (\mathbf{u}^a\cdot \nabla)\mathbf{u}^a + \frac{1}{Ro^a} \hat{\mathbf{z}} \times \mathbf{u}^a + \frac{1}{C^a} \nabla \theta^a = {\nu}^a \Delta \mathbf{u}^a, \\
        &\frac{\partial \theta^a}{\partial t} + \nabla \cdot (\mathbf{u}^a \theta^a) = \gamma(\theta^a - \theta^o) + \eta^a \Delta \theta^a,\\
    \text{Ocean}: \ &\frac{\partial \mathbf{u}^o}{\partial t} + (\mathbf{u}^o\cdot \nabla)\mathbf{u}^o + \frac{1}{Ro^o} \hat{\mathbf{z}} \times \mathbf{u}^o + \frac{1}{Ro^o} \nabla p^o = \sigma(\mathbf{u}^o - \mathbf{u}_{sol}^a) + \nu^o \Delta \mathbf{u}^o,\\
    & \nabla \cdot \mathbf{u}^o = 0,\\
    &\frac{\partial \theta^o}{\partial t} + \mathbf{u}^o \cdot \nabla \theta^o = \eta^o \Delta \theta^o.
\end{align*}
$$

`Model description:` We solved the climate model equations on a rectangular domain with periodic boundary conditions in the $x$ direction and free-slip velocity conditions on the boundaries in the $y$ direction. The physical dimensions of the domain are $27237$ km (in $x$) and $3891$ km (in $y$), which, after non-dimensionalization, correspond to $\Omega = [0,7] \times [0,1]$. 

*Table 1: Grid parameters for the atmosphere and ocean components of the climate model*

| Parameters      | Grid           | 
| :-------------: |:-------------:| 
| Number of elements, $N_x \times N_y $ |$896 \times 128$ |
| Smallest element size, $\Delta x$     |$1/128 \ (\sim 30 \ \text{km})$ | 
| Time-step size, $\Delta t$  | $0.010 \ (\sim 8 \ \text{min.})$  |  
| Eddy viscosity, $\nu^a, \nu^o $ |   $1/(8 \times 10^4)$        |
| Diffusion coefficient, $\eta^a, \eta^o $ | $1/(8 \times 10^4)$ | 


`Simulation results:`

<img src="/assets/img/clim_at_t0.png" alt="Initial state of the climate model" width="600"/>

*Figure 2: Initial atmospheric temperature (top), atmospheric velocity (middle), and ocean temperature (bottom) fields at $t=0$. The ocean velocity is set to zero at $t=0$.*

<img src="/assets/img/clim_at_t25.png" alt="State of the climate model at t=25" width="600"/>

*Figure 3: Atmospheric (top two) and oceanic (bottom two) velocity and temperature fields at $t = 25$ for the deterministic climate model simulation.*

<video width="600" controls title="Evolution of vorticity in the high-resolution deterministic climate model">
  <source src="/assets/video//atm_vort_coup_model_t25_to_t45.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>
*Video 2: Evolution of atmosphere vorticity field from $t = 25$ on wards. The number of small, medium, and large eddies remains roughly constant over the time interval.*







