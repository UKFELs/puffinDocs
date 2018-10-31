# Building Puffin on Scafell Pike at the Hartree Centre

'Scafell Pike' is a Bull-Atos Sequana system used for production runs at the Hartree Centre, with architecture described [here](http://community.hartree.stfc.ac.uk/wiki/site/admin/sequana%20-%20further%20info.html).

These instructions use the default Intel compilers and Intel MPI, and use the system-provided FFTW3 and HDF5 libraries.

First, load the necessary modules:
```
module load intel
module load intel_mpi
module load cmake
```

Note that the pre-built `fftw3` and `hdf5` libraries are **not** being loaded here. Unfortunately, the versions of `fftw3` and `hdf5` available as pre-compiled modules cause synchronization errors when working across multiple nodes (*possibly* due to using different versions of Intel MPI). Whatever the reason, we must build our own versions of `fftw3` and `hdf5`.

Information on the environment for Scafell Pike is [here](http://yukon.dl.ac.uk:8080/wiki/site/admin/sfp_jobs.html), with more detailed info on staging executables and data [here](http://yukon.dl.ac.uk:8080/wiki/site/admin/power8jobs.html). Job submission must be from the `$HCBASE` directory (or a subdirectory therein). However, you are recommended/required to store executables and data on the `$HCCDS` drive. So, these must be copied to the `$HCBASE` drive for job submission. You can 'stage' data from `$HCCDS` to your run on Scafell Pike directly from there. Because we are building `fftw3` and `hdf5`, and not linking statically, we are have to somehow move or stage all of the libraries being used. You will have to choose which is best. For this, I built the libraries on `$HCCDS`, and then copied them to `$HCBASE`, and built Puffin on `$HCBASE`. It may be that this is not the 'recommended' way of building software for Scafell Pike.

Fortunately, building both `fftw3` and `hdf5` is relatively simple. Grab the sources ([fftw3](http://www.fftw.org/download.html) and [hdf5](https://www.hdfgroup.org/downloads/hdf5/source-code/)) then configure, make, and make install. After loading the modules as above, for `hdf5`, go into the top-level of the unzipped source and do:

```
./configure --prefix=$HCCDS/fftw3 --enable-mpi --enable-openmp
make
make install
```

This will build the `fftw` libraries in your `$HCCDS/fftw3` directory. Similarly, do 

```
CC=mpiicc CPC=mpiicpc FC=mpiifort F90=mpiifort F77=mpiifort ./configure --enable-parallel --enable-fortran --prefix=$HCCDS//hdf5
make
make install
```

for `hdf5`, in the root of its unzipped source.

As explained above, the libraries must be launched from the `$HCBASE` directory, so we have been copying the built libraries to this drive for building and linking to Puffin *i.e.* do

```
cp -r $HCCDS/fftw3 $HCBASE/
cp -r $HCCDS/hdf5 $HCBASE/
```

Then to build Puffin, we do the usual `CMake` and build commands (outlined [here](BUILD.md)):

```
cmake <path to Puffin source root> -DENABLE_PARALLEL:BOOL=1 -DCMAKE_PREFIX_PATH:FILEPATH="$HCBASE/hdf5;$HCBASE/fftw3" -DCMAKE_INSTALL_PREFIX:FILEPATH=$HCBASE/puffin
make
make install
```

which builds Puffin in the `$HCBASE/puffin` directory.
