Custom CMake build for MCNP
===========================

The build system that ships with the MCNP source code from RSICC is often
annoying to use, requiring users to use undocumented config commands, or even
broken. This repository contains CMake files that are intended to replace MCNP's
build system. The versions of MCNP supported are
* 514 (MCNP5 version 5.1.40),
* 515 (MCNP5 version 5.1.50 or 5.1.51),
* 516 (MCNP5 version 5.1.60),
* X27 (MCNPX version 2.7.0),
* 602 (MCNP6 version 6_beta2),
* 610 (MCNP6 version 6.1), and
* 611 (MCNP6 version 6.1.1beta).

Support for MCNP6 version 6.2 will be added shortly after it becomes available
from RSICC.

Build options
-------------

The following build options control which version of MCNP are built.

* ``-DBUILD_MCNP514``  Build MCNP5 version 5.1.40 (ON/OFF; default is OFF)
* ``-DBUILD_MCNP515``  Build MCNP5 version 5.1.50 or 5.1.51 (ON/OFF; default is OFF)
* ``-DBUILD_MCNP516``  Build MCNP5 version 5.1.60 (ON/OFF; default is OFF)
* ``-DBUILD_MCNPX27``  Build MCNPX version 2.7.0 (ON/OFF; default is OFF)
* ``-DBUILD_MCNP602``  Build MCNP6 version 6_beta2 (ON/OFF; default is OFF)
* ``-DBUILD_MCNP610``  Build MCNP6 version 6.1 (ON/OFF; default is OFF)
* ``-DBUILD_MCNP611``  Build MCNP6 version 6.1.1beta (ON/OFF; default is OFF)

The following build options control features that apply to all version of MCNP.

* ``-DCMAKE_BUILD_TYPE``        Build configuration (i.e. Release, Debug, RelWithDebInfo; default is Release)
* ``-DCMAKE_C_COMPILER``        C compiler (i.e. gcc, icc)
* ``-DCMAKE_CXX_COMPILER``      C++ compiler (i.e. g++, icpc)
* ``-DCMAKE_Fortran_COMPILER``  Fortran compiler (i.e. gfortran, ifort)
* ``-DMCNP_PLOT``               Build with plotting capability (ON/OFF; default is OFF)
* ``-DOPENMP_BUILD``            Build with OpenMP support (ON/OFF; default is OFF)
* ``-DMPI_BUILD``               Build with MPI support (ON/OFF; default is OFF)

Build example
-------------

```
$ mkdir MCNP
$ cd MCNP
$ git clone https://github.com/ljacobson64/MCNP_CMake
<manually copy the MCNP source code to the correct directories>
$ ln -s MCNP_CMake src
$ mkdir bld
$ cd bld
$ cmake ../src -DBUILD_MCNP514=ON \
               -DBUILD_MCNP515=ON \
               -DBUILD_MCNP516=ON \
               -DBUILD_MCNPX27=ON \
               -DBUILD_MCNP602=ON \
               -DBUILD_MCNP610=ON \
               -DBUILD_MCNP611=ON \
               -DMCNP_PLOT=ON \
               -DOPENMP_BUILD=ON \
               -DMPI_BUILD=ON \
               -DCMAKE_INSTALL_PREFIX=${install_prefix}
make
make install
```

Correct directory structure
---------------------------

```
$ tree -d
.
├── cmake
├── MCNP514
│   └── Source
│       ├── dotcomm
│       │   ├── include
│       │   └── src
│       │       └── internals
│       │           ├── mpi
│       │           └── pvm
│       └── src
├── MCNP515
│   └── Source
│       ├── dotcomm
│       │   ├── include
│       │   └── src
│       │       └── internals
│       │           ├── mpi
│       │           └── pvm
│       └── src
├── MCNP516
│   └── Source
│       ├── dotcomm
│       │   ├── include
│       │   └── src
│       │       └── internals
│       │           └── mpi
│       └── src
├── MCNP602
│   └── Source
│       ├── dedx
│       ├── dotcomm
│       ├── fluka89
│       ├── hexs
│       ├── import
│       ├── lcs
│       ├── meshtal
│       ├── regl
│       ├── spabi
│       └── src
│           ├── partisn
│           └── utils
├── MCNP610
│   └── Source
│       ├── dedx
│       ├── hexs
│       ├── import
│       ├── lcs
│       ├── meshtal
│       ├── regl
│       ├── spabi
│       └── src
│           ├── partisn
│           └── utils
├── MCNP611
│   └── Source
│       ├── dedx
│       ├── hexs
│       ├── import
│       │   └── cgm
│       ├── lcs
│       ├── meshtal
│       ├── regl
│       ├── spabi
│       └── src
│           ├── partisn
│           └── utils
├── MCNPX27
│   └── Source
│       ├── include
│       │   ├── cem
│       │   ├── dedx
│       │   ├── fluka89
│       │   ├── globals
│       │   ├── gridconv
│       │   ├── hexs
│       │   ├── htape3x
│       │   ├── incl
│       │   ├── lcs
│       │   ├── mcnpf
│       │   ├── trx
│       │   └── xsex3
│       └── mcnpx
│           ├── dedx
│           ├── f77main
│           ├── fluka89
│           ├── gvaviv
│           ├── hexs
│           ├── histp
│           ├── lcs
│           ├── mcnpc
│           ├── mcnpf
│           ├── meshtal
│           └── spabi
└── patch
```
