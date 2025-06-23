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
    \text{Atm.}:\quad & \mathrm{d} \mathbf{u}^a + ((\mathbf{u}^a \mathrm{d} t + {\sum_i \boldsymbol{\xi}_i \circ \mathrm{d} W^i})\cdot \nabla) \mathbf{u}^a + \frac{1}{Ro^a} \hat{\mathbf{z}} \times (\mathbf{u}^a\, \mathrm{d}t + {\sum_i \boldsymbol{\xi}_i \circ \mathrm{d} W^i}) \\
    & + {\sum_i \left( \sum_{j=1}^2 u_j^a \nabla \xi_{i,j} + \frac{1}{Ro^a}\nabla(\boldsymbol{\xi}_i \cdot \mathbf{R}) \right) \circ \mathrm{d} W^i} \\
    &= \left( -\frac{1}{C^a} \nabla \theta + \frac{1}{Re^a} \Delta \mathbf{u}^a \right) \mathrm{d}t, \\
    \mathrm{d} \theta^a + \nabla\cdot\left(\theta^a (\mathbf{u}^a\, \mathrm{d}t + {\sum_i \boldsymbol{\xi}_i \circ \mathrm{d} W^i})\right) &= \left(\gamma(\theta^a - \theta^o) + \frac{1}{Pe^a} \Delta \theta^a \right)\mathrm{d}t, \\
    \text{Ocean}:\quad \frac{\partial \mathbf{u}^o}{\partial t} + (\mathbf{u}^o \cdot \nabla)\mathbf{u}^o + \frac{1}{Ro^o} \hat{\mathbf{z}} \times \mathbf{u}^o + \frac{1}{Ro^o} \nabla p^a &= \sigma(\mathbf{u}^o - \mathbb{E}\mathbf{u}_{\text{sol}}^a) + \frac{1}{Re^o} \Delta \mathbf{u}^o, \\
    \nabla \cdot \mathbf{u}^o &= 0, \\
    \frac{\partial \theta^o}{\partial t} + \mathbf{u}^o \cdot \nabla \theta^o &= \frac{1}{Pe^o} \Delta \theta^o.
\end{align*}
$$
where the vector variable $\mathbf{u}$ and the scale variables $\theta$ and $p$ (with superscripts for the atmosphere and ocean components) denote the velocity, potential temperature, and pressure fields, respectively. The atmospheric temperature is coupled to the ocean temperature through the term $\gamma (\theta^a - \theta^o)$ representing the transfer of heat from the ocean to the atmosphere. The atmosphere and ocean velocities are coupled through the term $\sigma (\mathbf{u}^o - \mathbf{u}^a_{sol})$ which models the shear stress exerted by atmospheric winds on the ocean surface. 

Stochastic terms (shown in red) which model the small-scales can be estimated using the satellite data. In our work, we estimate the stochastic terms (mainly $\boldsymbol{\xi}_i$) using statistical analysis of velocity data obtained from high-resolution simulation of the deterministic model. 

## Key simulations





