---
title: 'Standing on the shoulders of giants'
date: 2018-08-07
permalink: /posts/2013/08/prerosettacon-pyrosetta/
tags:
  - python
  - rosetta
  - molecular modeling
---

Yesterday and the day before were what is becoming known as "PreRosettaCon". Essentially, it's a two-day meeting in which scientists from all over the world who are developing new methods in Rosetta or otehrwise rely on it for their research come together, discuss issues, make plans to solve them. There's also a lot of discussion surrounding big new developments and we try to determine what we need to do to make sure no one is left out.

We made solid plans to develop a stable, pythonic API for PyRosetta (python bindings for the Rosetta C++ code) that should prevent old scripts from becoming useless, and presented functional conda-installable builds for both Linux and macOS. It is my hope that making it easier to reference installed version numbers and having a well-defined way of installing speciic versions will lead to new tools that use PyRosetta like any other module, and, importantly, dramatically simplify the effort required to maintain reproducibility of results produced by our software.

One of the reasons there is so much excitement around PyRosetta is that it can be used in conjunction with countless packages from the broader scientific community. Being able to use other people's solutions to common problems encourages us to think more abstractly and to focus our development efforts on code more closely-related to protein modeling. It lets us stand on the shoulders of giants. Along with Alex Ford, I presented some work to better intergrate PyRosetta with commonly used packages in the scientific world. Chief among these integrations is our new compatibilty with `dask` for job distribution. Check out a simple demo in [this GitHub repo](https://github.com/RosettaCommons/pyrosettascripts_demo).
