---
title: 'Parametric disasters'
published: 2018-09-03
excerpt: "I recently got a new computer and I have been (slowly) going through my old files to try to some order around here. So, while I was doing this kind of twenty-first century upkeep, I stumbled across a file called “nope_nope_nope.mov”. Here’s what was in that file..."
permalink: /posts/2018/08/parametric-disasters/
tags:
  - python
  - rosetta
  - molecular modeling
---

I recently got a new computer and I have been (slowly) going through my old files to try to some order around here. So, while I was doing this kind of twenty-first century upkeep, I stumbled across a file called “nope_nope_nope.mov”. Here’s what was in that file:

![alt text](https://weitzner.github.io/files/mov/helical_disaster.gif "It's like a weird protein jellyfish, man.")

There’s another one called “strand_fail.mov” that looks like this:

![alt text](https://weitzner.github.io/files/mov/strand_disaster.gif "I think I could watch this all day.")

What each of these movies show is a failed initial attempt at extending the parametric bundle design methods used in Rosetta. A little while ago, Vikram Mulligan and I sat down to think about what would be needed to describe a β barrel. We started off noting that a strand could be thought of as a helix in which every residue flips 180º, and that we would need to describe a "squishing" parameter to describe non-circular barrel systems.

Vikram recently moved on to the [Flatiron Institute](https://www.simonsfoundation.org/flatiron/) in New York, but this was a fun little project that kind of went nowhere so I thought I would share it here. Also, he took really detailed notes and made a lot of pretty pictures and it would be a shame for the world to not have them.

## First, some background
We have had some success [designing helical bundles](https://doi.org/10.1126/science.1257481) from [parametric equations](https://doi.org/10.1107/S0365110X53001952) first developed by Francis Crick. These equations enable us to calculate the coordinates of each helical residue's α carbon using descriptors with clear physical meanings, which allows us to specify geometric properties or requirements of a helical bundle and quickly trace out a backbone based on those requirements.

The equations are:

\begin{align}
X(t) & = R_0 \cos(\omega_0 t + {\phi_0}^\prime) + R_1 \cos( \omega_0 t + {\phi_0}^\prime) \cos(\omega_1 t + \phi_1) - R_1 \cos(\alpha) \sin(\omega_0 t + {\phi_0}^\prime) \sin(\omega_1 t + \phi_1) \\
Y(t) & = R_0 \sin(\omega_0 t + {\phi_0}^\prime) + R_1 \sin(\omega_0 t + {\phi_0}^\prime) \cos(\omega_1 t + \phi_1) + R_1 \cos(\alpha) \cos(\omega_0 t + {\phi_0}^\prime) \sin(\omega_1 t + \phi_1) \\
Z(t) & = (\omega_0 R_0 / \tan(\alpha)) t - R_1 \sin(\alpha) \sin(\omega_1 t + \phi_1) + \Delta z
\end{align}

Grigoryan and DeGrado [described the parameters](https://doi.org/10.1016/j.jmb.2010.08.058) as:
* Superhelical radius, $R_0$
* Superhelical frequency/twist, $\omega_0$
* Superhelical phase, $\phi_0$
* Helical radius, $R_1$
* Helical frequency/twist, $\omega_1$
* Helical phase, $\phi_1$
* Offset along the $z$ axis, $\Delta z$
* Pitch angle, $\alpha = \arcsin(R_0 \omega_0 / d)$, where $d$ is the distance between residues
* Superhelical phase (decoupled from the $z$ offset), ${\phi_0}^\prime = \phi_0 + \Delta z \tan(\alpha) / R_0$

Calculations are made a little simpler by holding $R_1$ and $d$ fixed at the values for ideal helices (1.51 and 2.26 Å), and by distributing helices evenly about the $z$ axis, which gives $\phi_0$ legal values of $\\{0, 2\pi/n, 4\pi/n... 2(n-1) \pi/n\\}$.

## How can we incorporate a "squish"?
One of the simplifying assumptions that is used in the equations above is that all parameters are constants. But when we want to model barrels with non-circular cross sections, that simplification leaves the room. In this case, the superhelical radius will depend on a new parameter, $\epsilon$, the eccentricity of the elipse. Here's a photo of a white board where we derived this:

![alt text](https://weitzner.github.io/files/img/wb_math.png "It's possible that this was not the first time this was written up.")

With the new $R_0$ term, we can stretch barrels in one dimension and evaluate metrics like hydrogen bonding along the way:

![alt text](https://weitzner.github.io/files/mov/strand_sample_along_axis.gif "Notice how the hydrogen bonds appear when the strands are arranged appropriately.")

Here's what it looks like normal to the barrel axis:

![alt text](https://weitzner.github.io/files/mov/strand_sample_orth.gif "Here's a side view.")

And then, finally, one can generate parameters and use some metric to perform monte carlo sampling of a parametrically-designed β barrel.

![alt text](https://weitzner.github.io/files/mov/b_barrel_wiggle.gif "Look at all that hydrogen bond goodness!")

Thanks for all the fun times and good work, Vikram!
