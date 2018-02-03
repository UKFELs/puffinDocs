# Puffin Documentation

A Free Electron Laser (FEL) is a device in which an ultra-fast electron beam, travelling close to the speed of light, is made to wiggle from side to side by passing it through a magnetic device known as an undulator, which enables it to amplify a co-propagating radiation field by many orders of magnitude. The FEL is the world's premier source of coherent X-Rays, with national facilites in the U.S., Germany, Japan, Switzerland and more fully booked by physicists and chemists trying to understand matter on the ultra-fast, ultra-small scale.

The 'usual' way of doing FEL theory and numerical codes involves a number of approximations, including:

  - Averaging out the fast wiggle motion of the electrons
  - Assuming the radiation field varies slowly over one radiation wavelength (Slowly Varying Envelope Approximation, or SVEA)
  - Confining the electrons within self-contained slices (usually a resonant radiation wavelength long) with periodic boundary conditions

The above approximations are usually perfectly valid, but there are some regimes in which they may not be applied, or, at least, the application of them is questionable. Puffin, being a so-called 'unaveraged' FEL code, has been written to allow investigation into these somewhat esoteric modes of operation, and to test concepts that other FEL codes cannot. Lack of the above restrictions results in the capability of modelling the full radiation and electron bandwidth, with the drawback of increased computation time, necessitating a need for parallel computation on large HPC clusters for fully temporal 3D runs. Puffin is not free of all assumptions, however: we still neglect the backwards propagating wave in the system, we make the paraxial approximation, and neglect space-charge and wakefields.

Due to the nature of the code, and the likely use cases for such a code, we have attempted to create a resource which is a flexible tool for numerical scientific research, while still containing enough 'realistic'  components to enable reasonable modelling of a current or future facility.

## Code Description

Puffin is written in modern Fortran, using MPI and OpenMP.

## How to Install

The source code is hosted here, along with binaries for Ubuntu 16.04 in the releases section.

To build from source, Puffin uses CMake and SciMake to detect the relevant packages on your machine and generate a Makefile.

See here for more info.

## How to Run

Once installed, Puffin must be invoked with MPI, passing it the main input file (see section ), here called main.in

`mpirun -np 2 puffin main.in`

which will launch Puffin on 2 MPI processes.
