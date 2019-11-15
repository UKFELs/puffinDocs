# Building Puffin on Ubuntu and other similar Linux
The below instruction of Puffin install is meant for Ubuntu, however it can be successfully applied on other Linux branches (e.g. Manjaro).
The packages required by Ubuntu (and other Linux) include:

- gfortran (gfortran)
- OpenMPI (libopenmpi-dev, openmpi-bin - for Ubuntu, other distributions often use different package names)
- Cmake (cmake)

In general, you need to be able to issue commands like: `mpirun, mpicc, mpif90, cmake`. When trying to issue such command you should only see message that the source input file is missing but the command should execute.
Some version of Ubuntu have precompiled `HDF5` nad `FFTW3` libraries. However, the libraries are often not fully compatibile with Puffin. The most general approach to build Puffin is to build first your own `HDF5` and `FFTW3` libraries. Whatever the reason, we must build our own versions of `FFTW3` and `HDF5`.

Fortunately, building both `FFTW3` and `HDF5` is relatively simple. Grab the sources ([FFTW3](http://www.fftw.org/download.html) and [HDF5](https://www.hdfgroup.org/downloads/hdf5/source-code/)) then configure, make, and make install. After loading the modules as above, for `HDF5`, go into the top-level of the unzipped source and do:

```
./configure --prefix=$/my_home_directory/my_fftw3_install_directory --enable-mpi --enable-openmp
make
make install
```

This will build the `FFTW3` libraries in your `/my_home_directory/my_fftw3_install_directory` directory. Similarly, do 

```
CC=mpiicc CPC=mpiicpc FC=mpiifort F90=mpiifort F77=mpiifort ./configure --enable-parallel --enable-fortran --prefix=/my_home_directory/my_hdf5_install_directory
make
make install
```

for `HDF5`, in the root of its unzipped source.

Then to build Puffin, we do the usual `CMake` and build commands (outlined [here](BUILD.md)):

```
cmake <path to Puffin source root> -DENABLE_PARALLEL:BOOL=1 -DCMAKE_PREFIX_PATH:FILEPATH="/my_home_directory/my_hdf5_install_directory;/my_home_directory/my_fftw3_install_directory" -DCMAKE_INSTALL_PREFIX:FILEPATH=/my_home_directory/my_puffin_install_directory
make
make install
```

which builds Puffin in the `/my_home_directory/my_puffin_install_directory` directory.
