# Interface for conversion between hdf5 and kdb+ data 

[![GitHub release (latest by date)](https://img.shields.io/github/v/release/kxsystems/hdf5?include_prereleases)](https://github.com/kxsystems/hdf5/releases) [![Travis (.org) branch](https://img.shields.io/travis/kxsystems/hdf5/master?label=travis%20build)](https://travis-ci.org/kxsystems/hdf5/branches)

## Introduction

This interface provides a mechanism for kdb+ users to interact with and create HDF5 datasets. The interface is a thin wrapper for kdb+ around the HDF Group's C api for HDF5, outlined in full [here](https://support.hdfgroup.org/HDF5/doc/RM/RM_H5Front.html)

This is part of the [_Fusion for kdb+_](http://code.kx.com/q/interfaces/fusion/) interface collection.

## New to kdb+ ?

Kdb+ is the world's fastest time-series database, optimized for ingesting, analyzing and storing massive amounts of structured data. To get started with kdb+, please visit https://code.kx.com/q/learn/ for downloads and developer information. For general information, visit https://kx.com/

## New to HDF5 ?

Hierarchical Data Format 5 (HDF5) is a file format designed specifically for the storage and organization of large amounts of data.

In many ways, HDF5 acts like a hierarchical file system similar to that used by linux or windows. This structure contains two major objects:

1. Datasets - Multidimensional arrays of homogeneously-typed data, or compound data containing a mixture of types. Datasets are similar to files within a traditional POSIX file system.
2. Groups - Container structures holding datasets or other groups. They function similarly to directories within a traditional POSIX file system.

There are a number of secondary objects and structures, which add complexity to the format. In doing so, they allow the format to be used for a wider range of use cases

* Attributes: These allow metadata information to be associated with a dataset or group e.g. associate the date of data collection with a group, or the temperature when a set of results was collected.
* Linking functionality: Like a traditional POSIX file system it is possible to create links between objects (hard/soft/external). These allow datasets or groups relevant to multiple experiments to be accessed via more intuitive routes.

If you have any HDF5 related questions, you can raise them on the [HDF Forum](https://forum.hdfgroup.org/).


## Installation

### Requirements

* kdb+ ≥ 3.5 64-bit
* [HDF5 C api](https://support.hdfgroup.org/HDF5/doc/H5.intro.html) ≥ 1.10

### Third-Party Library Installation

The following outlines instructions for installing the HDF5 group's C api for supported architectures.

**Linux**
- Download a supported release of hdf5 and install, instructions are provided [here](https://support.hdfgroup.org/HDF5/HDF5-FAQ.html#10).

**MacOS**
- Run `brew install hdf5`

### Installing a release

It is recommended that a user install this interface through a release. Installation of the interface from a release is completed in a number of steps

1. Ensure you have downloaded/installed the HDF5 C api following the instructions [here](#third-party-library-installation)
2. Download a release from [here](https://github.com/KxSystems/hdf5/releases) for your system architecture.
3. Add the location of the 'lib' directory for the HDF5 C api to `LD_LIBRARY_PATH`/`DYLD_LIBRARY_PATH` for Linux or MacOS respectively.

	```
	## Linux
	export LD_LIBRARY_PATH=/usr/local/hdf5-c-api/lib/:$LD_LIBRARY_PATH

	## MacOS
	export DYLD_LIBRARY_PATH=/Users/bob/hdf5-c-api/lib/:$DYLD_LIBRARY_PATH
	```

4. Install required q executable script `hdf5.q` and binary file `lib/libhdf5.so` to `$QHOME` and `$QHOME/[ml](64)` respectively by executing the following from the Release directory

	```
	chmod +x install.sh

	./install.sh
	```

### Building interface from source and install

In order to successfully build and install this interface, the following environment variables must be set:

1. `HDF5_HOME` = Location of the HDF5 C api installation (directory containing `/include` and `/lib` subdirectories).
2. `QHOME` = Q installation directory (directory containing `q.k`).

* Create a directory from which the execute the CMAKE command and move into this directory

```bash
mkdir build && cd build
```

* Execute the `cmake` instructions

```bash
cmake ..
```

* generate the `libhdf5.so` binary

```bash
make
```

* Install the `libhdf5.so` binary into `$QHOME/[ml]64` and `hdf5.q` into `$QHOME`

```bash
make install
```
 
## Unsupported Functionality

This interface is in active developement and as such there are a number of use-cases that are currently not supported.

- Use of this interface on Windows 64-bit systems
- Creation of compressed datasets
- Access to unlimited datasets
- Interaction with HDF5 images

If your use case requires the above functionality to be available, please open an issue [here](https://github.com/KxSystems/hdf5/issues). If you are capable, please consider contributing to the project.

## Documentation

Documentation outlining the functionality available for this interface can be found [here](https://code.kx.com/q/interfaces/hdf5).

## Status

The HDF5 interface is provided here under an Apache 2.0 license.

If you find issues with the interface or have feature requests please consider raising an issue [here](https://github.com/KxSystems/hdf5/issues).

If you wish to contribute to this project please follow the contributing guide [here](https://github.com/KxSystems/hdf5/blob/master/CONTRIBUTING.md).
