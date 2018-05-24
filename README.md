[![Build Status](https://travis-ci.org/balintfodor/sba.svg?branch=master)](https://travis-ci.org/balintfodor/sba)

# SBA 

version 1.6
 
By Manolis Lourakis

Institute of Computer Science 
Foundation for Research and Technology - Hellas
Heraklion, Crete, Greece

## General

This is sba, a copylefted C/C++ implementation of generic bundle adjustment
based on the sparse Levenberg-Marquardt algorithm. sba can support a wide
range of manifestations/parameterizations of the multiple view reconstruction
problem such as arbitrary projective cameras, partially or fully intrinsically
calibrated cameras, exterior orientation (i.e. pose) estimation from fixed 3D
points, etc. sba can be downloaded from [http://www.ics.forth.gr/~lourakis/sba](http://www.ics.forth.gr/~lourakis/sba)

sba relies on lapack for solving the augmented normal equations arising in the
course of the Levenberg-Marquardt algorithm. if you don't already have lapack,
I suggest getting clapack from http://www.netlib.org/clapack.
Directory demo contains eucsbademo, a working example of using sba for Euclidean
bundle adjustment.

More details regarding sba can be found in ICS/FORTH Technical Report No. 340
entitled "The Design and Implementation of a Generic Sparse Bundle Adjustment
Software Package Based on the Levenberg-Marquardt Algorithm", by M.I.A. Lourakis
and A.A. Argyros (available from [http://www.ics.forth.gr/~lourakis/sba](http://www.ics.forth.gr/~lourakis/sba))

In case that you use sba in your published work, please include a reference to
the above TR:

@techreport{lourakis04,
    author={M.I.A. Lourakis and A.A. Argyros},
    title={The Design and Implementation of a Generic Sparse Bundle Adjustment Software Package
           Based on the Levenberg-Marquardt Algorithm}
    institution={Institute of Computer Science - FORTH},
    address={Heraklion, Crete, Greece},
    number={340},
    year={2004},
    month={Aug.},
    note={Available from \verb+http://www.ics.forth.gr/~lourakis/sba+}
}

## Files

- _sba_levmar.c_: SBA expert driver routines
- _sba_levmar_wrap.c_: simple wrappers around the routines in sba_levmar.c
- _sba_lapack.c_: LAPACK-based linear system solvers (LU, QR, SVD, Cholesky, Bunch-Kaufman)
- _sba_crsm.c_: CRS sparse matrix manipulation routines
- _sba_chkjac.c_: routines for verifying the correctness of user-supplied jacobians
- _sba.h_: Function prototypes & related data structures
- _demo/*_: Euclidean BA demo; see demo/README.txt for more details
- _matlab/*_: sba MEX-file interface; see matlab/README.txt for more details
- _utils/*_: Various utilities; see utils/README.txt for more details

## Compiling

The library compilation settings can be generated using CMake.
The options are:
- _BUILD_SHARED_LIBS_, default OFF
- _BUILD_DEMO_, default ON
- _USE_MKL_, default OFF, tells CMake to use Intel MKL libraries. MKL environment should be already loaded for this to work.

Options can be set on the command line using `-D<option_name>=<ON or OFF>`.

### Basic compilation
From the library root folder:

```
mkdir build
cd build
cmake ..
make
```

Send your comments/bug reports to lourakis@ics.forth.gr
