# Building Puffin on Jureca

These instructions use the default Intel compilers and Intel MPI, and use the system-provided FFTW3 and HDF5 libraries.

First, load the necessary modules:
```
module load intel-para
module load CMake
module load FFTW/3.3.7
module load HDF5/1.8.20
```

Then, define some environment variables, just in case (not sure if this is strictly needed...)

```
export CC=mpicc
export CXX=mpicxx
export F90=mpif90
export F77=mpif90
export F9X=mpif90
export FC=mpif90
export MPICC=mpicc
export MPICXX=mpicxx
export MPIF90=mpif90
export MPI_CXX=mpicxx
```

Then we do the usual `CMake` and build commands outlined [here](BUILD.md)
```
cmake -DENABLE_PARALLEL:BOOL=TRUE -DCMAKE_INSTALL_PREFIX:PATH=/homeb/username/puffininstall -DFftw3_ROOT_DIR='/usr/local/software/jureca/Stages/2018a/software/FFTW/3.3.7-ipsmpi-2018a' -DHdf5_ROOT_DIR='/usr/local/software/jureca/Stages/2018a/software/HDF5/1.8.20-ipsmpi-2018a/' /homeb/username/puffinbase
```
then just `make && make install`
