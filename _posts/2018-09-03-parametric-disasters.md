---
title: 'Parametric disasters'
published: 2018-09-03
excerpt: "Parametric disasters"
permalink: /posts/2018/08/parametric-disasters/
tags:
  - python
  - rosetta
  - molecular modeling
---

We have had some success [designing helical bundles](https://doi.org/10.1126/science.1257481) from [parametric equations](https://doi.org/10.1107/S0365110X53001952) first developed by Francis Crick. These equations enable us to calculate the coordinates of each helical residue's alpha carbon using descriptors with clear physical meanings, whiich allows us to specify geometric properties or requirements of a helical bundle and quickly trace out a backbone based on those requirements.

The equations are:
$x = R_0 \cos(\omega_0 t + {\phi_0}^\prime) + R_1 \cos( \omega_0 t + {\phi_0}^\prime) \cos(\omega_1 t + \phi_1) - R_1 \cos(\alpha) \sin(\omega_0 t + {\phi_0}^\prime) 
sin(\omega_1 t + \phi_1)$
$y = R_0 \sin(\omega_0 t + {\phi_0}^\prime) + R_1 \sin(\omega_0 t + {\phi_0}^\prime) \cos(\omega_1 t + \phi_1) + R_1 \cos(\alpha) \cos(\omega_0 t + {\phi_0}^\prime) \sin(\omega_1 t + \phi_1)$
$z = (\omega_0 R_0 / \tan(\alpha)) t - R_1 \sin(\alpha) \sin(\omega_1 t + \phi_1) + \Delta z$

Grigoryan and DeGrado [described the parameters](https://doi.org/10.1016/j.jmb.2010.08.058) as: 
* $R_0$  Superhelical radius
* $\omega_0$  Superhelical frequency/twist
* $\phi_0$  Superhelical phase
* $R_1$  Helical radius
* $\omega_1$  Helical frequency/twist
* $\phi_1$  Helical phase
* $\Delta z$  Offset along the $z$ axis
* $\alpha = \arcsin(R_0 \omega_0 / d)$, where $d$ is the distance between residues, pitch angle
* ${\phi_0}^\prime = \phi_0 + \Delta z \tan(\alpha) / R_0$  Superhelical phase (decoupled from the $z$ offset)

Calculations are made a little simpler by holding $R_1$ and $d$ fixed at the values for ideal helices (1.51 and 2.26 Å), and by distributing helices evenly about the $z$ axis, which gives $\phi_0$ legal values of $\\{0, 2\pi/n, 4\pi/n... 2(n-1) \pi/n\\}$.

<video width='720' height='480' preload='none' loop autoplay>
   <source src='https://weitzner.github.io/files/helical_disaster.mov' type='video/mp4'/>
</video>


Also with strands:

<video width='720' height='550' preload='none' loop autoplay>
   <source src='https://weitzner.github.io/files/strand_disaster.mov' type='video/mp4'/>
</video>
