# Puffin Documentation

Welcome to the documentation for Puffin! Puffin (Parallel Unaveraged Fel INtegrator) is a massively parallel 3D numerical solver for a Free Electron Laser (FEL). Puffin can be found on Github [here](https://github.com/UKFELs/Puffin).

## Motivation

A Free Electron Laser (FEL) is a device in which an ultra-fast electron beam, travelling close to the speed of light, is made to wiggle from side to side by passing it through a magnetic device known as an undulator, which enables it to amplify a co-propagating radiation field by many orders of magnitude. The FEL is the world's premier source of coherent X-Rays, with national facilites in the U.S., Germany, Japan, Switzerland, China and more fully booked by a wide range of physicists, biologists, and chemists trying to understand matter on the ultra-fast, ultra-small scale.

The 'usual' way of doing FEL theory and numerical codes involves a number of approximations, including:

  - Averaging out the fast wiggle motion of the electrons
  - Assuming the radiation field varies slowly over one radiation wavelength (Slowly Varying Envelope Approximation, or SVEA)
  - Confining the electrons within self-contained slices (usually a resonant radiation wavelength long) with periodic boundary conditions

The above approximations are usually perfectly valid, but there are some regimes in which they may not be applied, or, at least, the application of them is questionable. Puffin, being a so-called 'unaveraged' FEL code, has been written to allow investigation into these somewhat esoteric modes of operation, and to test concepts that other FEL codes cannot. Lack of the above restrictions results in the capability of modelling the full radiation and electron bandwidth, with the drawback of increased computation time, necessitating a need for parallel computation on large HPC clusters for fully temporal 3D runs. Puffin is not free of all assumptions, however: we still neglect the backwards propagating wave in the system, we make the paraxial approximation, and neglect space-charge and wakefields.

## Features

Due to the nature of the code, and the likely use cases for such a code, we have attempted to create a resource which is a flexible tool for numerical scientific research, while still containing enough 'realistic'  components to enable reasonable modelling of a current or future facility. With this is mind, Puffin can model:

  - The full, broad bandwidth frequency spectrum, limited only by the Nyquist frequency of the mesh
  - Full electron beam transport
  - Transport of large energy spread beams through the undulator, and the radiation emitted from these beams
  - Tapered undulators
  - Fully 3D undulators, including modelling of the wiggler entries/exits and natural focusing
  - Common undulator line components including quads, chicanes, drifts etc. (modelled as point transforms)
  - Variably polarized undulators
  - Independent tuning of each undulator module

## Code Language

Puffin is written in modern Fortran, using MPI and OpenMP. It scales well up to many thousands of cores on large clusters, but smaller runs, in 1D or periodic mode, can usually be run locally. Post-processing scripts are in Python, using pytables and numpy.

## Documentation

This documentation consists of the following sections:

- [How to Install](BUILD.md)
- [How to run](howtorun.md)

There is also a [pdf manual on the Github repo](https://github.com/UKFELs/Puffin/blob/master/doc/manual.pdf).

## Attribution

Puffin was developed by Lawrence Campbell at the University of Strathclyde, with valuable contributions from Jonny Smith (Tech-X) and Cynthia Nam (University of Strathclyde). Puffin was originally reported [here](http://aip.scitation.org/doi/10.1063/1.4752743), and has undergone many improvements and extended its functionality significantly since then. It no longer uses an external linear solver package, and the only external packages now required are FFTW (version 3.3 onwards), and parallel HDF5 libraries. 

Please note Puffin is currently under active development (including this documentation). An 'official' release will be tagged soon.