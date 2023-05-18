---
layout: default
title: Installation
nav_order: 2
---

## Table of contents
{: .no_toc .text-delta }

1. TOC
{:toc}

## Dependencies 

To compile the code and run a typical simulation you will need working C/C++ compilers (for GNU version 4.x or later), [CMake](https://cmake.org/) tools and the following open-source libraries:

- GNU Scientific Library ([GSL](https://www.gnu.org/software/gsl/))
- Fastest Fourier Transform in the West ([FFTW3](http://www.fftw.org/)). To make us of the hybrid parallelisation it **needs to be installed** with the following options in the `./configure` step:
  -  `--enable-single` to allow for single precision 
  -  `--enable-mpi` for distributed resources (MPI processes)
  -  `--enable-openmp` for shared resources (multithreading)
  -  `--enable-avx`, `--enable-avx2` or `--enable-avx512` to exploit vector operations 
- Hierarchical Data Format ([HDF5](https://www.hdfgroup.org/solutions/hdf5/), version 1.10.2 or later). The `--enable-parallel` option **needs to be included** in the configuration to allow for parallel compression of large files.
- Message Passing Interface (MPI), version 3.0 or higher. Working examples are [Intel-MPI](https://www.intel.com/content/www/us/en/developer/tools/oneapi/mpi-library.html) and  [OpenMPI](https://www.open-mpi.org/). We have not tested [MPICH](https://www.mpich.org/).   
- NVIDIA Cuda [Toolkit](https://developer.nvidia.com/cuda-downloads), **for GPU runs only**. The installed version of the cuda libraries needs to be compatible with the drivers in the cards, this can be checked by typing `nvcc --version`. 

{: .note }

Most of these libraries  are typically available in most HPC environments, where they can be simply loaded by the command `module load <module_name>` etc. To make sure the parallel options are present type `module show <module_name>` and then check the configurations settings from the specified path.

{: .warning }
Note that jaxions only supports Intel CPUs or NVIDIA graphic cards (in GPU mode) at the moment. Typically one of these two options are available in HPC environments.

To visualise the output and to analyse the simulations some python packages need to be installed: 
- `numpy`
- `h5py` 
- `matplotlib` 

## Building the code

The installation workflow is summarised in the following: 

```
mkdir jaxionsdir ; cd jaxionsdir
git clone https://github.com/veintemillas/jaxions.git
mkdir build; cd build
cmake ../jaxions
make -j <num_threads>
```
If `cmake` fails to find the correct libraries, the explicit paths can be edited directly issuing the command `ccmake ./` inside the `jaxionsdir/build` directory.
The output of the compilation process is one library, `jaxionsdir/build/lib/libAxions.a`, and possibly several executable programs in the folder `jaxionsdir/build/tests/`.

The compilation can be speeded up by using multiple threads in the last step.

### Compilation options 

We recommend to compile with the most advanced AVX flags possible, no GPU, without NYX output and with just one time-integrator (RKN4 happens to be the best). This can be done in the `cmake` step by typing for example
```
cmake -D USE_AVX=ON USE_GPU=OFF ../jaxions
```
or by modifying the `CMakeLists.txt` file in `jaxionsdir/jaxions`.

The HDF5_PARALLEL_COMPRESSION compilation option needs to stay `ON` always. The `OFF` option is currently not supported.
{: .warning}

A list of compilation options can be found in the following table.

| Option       | Use ON            | 
|:-------------|:------------------|
| USE_PROP_LEAP | to compile 2-step leapfrog time-integrator |
| USE_PROP_MLEAP | to compile 8-step leapfrog time-integrator |
| USE_PROP_OM2 | to compile 3-step Omelyan symetric time-integrator |
| USE_PROP_OM4 | to compile 8-step Omelyan symetric time-integrator |
| USE PROP RKN4 | to compile optimised McLachlan time-integrator[^1]   |
| USE_AVX           | if your CPU supports Advance Vector eXtensions (AVX1.0) |
| USE_NN_BINS | to produce axion-spectra normalised with 1/$\omega$ for occupation numbers |
| USE_NYX_OUTPUT | to save configurations in AMReX format (in adition to HDF5), requires AMReX library | 
| USE_GPU | to evolve fields in the GPU (NVIDIA only) |
| USE_AVX | if your CPU supports Advance Vector eXtensions (AVX1.0) | 
| USE_AVX2 | if your CPU supports Advance Vector eXtensions with integers (AVX2.0) | 
| USE_AVX512 | if your CPU supports AVX512 | 
| USE_FMA | if your CPU supports Fused Multiplication-Addition FMA operations |

To check what operations your CPU supports you can issue the command 
```
sysctl -a | grep machdep.cpu.features
```

### Issues 

- On MacOS the default compiler is Apple clang, if however one wants to compile with the GNU or Intel compiler it needs to specified as in the following:
```
cmake -D CMAKE_C_COMPILER=/path/to/your/gcc ../jaxions
```

## Running on the GPU

---
[^1]: R. I. McLachlan and P. Atela, “The accuracy of symplectic integrators”, Nonlinearity 5 (1992) 541.
