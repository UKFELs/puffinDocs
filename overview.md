# Code Overview

Puffin represents the radiation field with a simple 3D mesh with equidistant sample nodes in each dimension, and the electron beam with a 6D distribution of macroparticles. The undulator fields are currently described analytically.

There are a number of different modes in Puffin which can be utilized to quickly test ideas without resorting to throwing a full 3D run on a cluster.

## Equations

The FEL equations which Puffin solves are in the radiation frame scaled to the FEL characteristic 
'cooperation length'.

## Dimensionality

Puffin can be run in 1D or 3D mode. It is important to note that the approximations which Puffin is absent of in relation to other FEL codes are essentially '1D' approximations, meaning that in many cases fundamental deviations from 'usual' codes and theory can be shown in 1D.

## Mesh setup

![Alt Text](pics/long_mesh.png "Radiation mesh and propagating beam.")

![Alt Text](pics/trans_mesh2.png "Setup of the radiation mesh and macroparticle beam in the transverse plane.")

## Temporal and Periodic Meshes

## Parallelism

Puffin uses a slab decomposition of the mesh, which is augmented with 'shared' sections to enable synchronization over neighbouring processes. Since we are in the radiation frame, macroparticles will always move from left to right.

![Alt Text](pics/mpi_mesh4.png "Equivalent 2D representation of MPI memory distribution.")

## Undulator Fields


