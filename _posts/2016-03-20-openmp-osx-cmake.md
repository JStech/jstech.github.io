---
layout: layout
title: OpenMP, OS X, and CMake
---

It took me far too long to figure out how to use OpenMP on OS X in a project
using CMake. Hopefully this will prove useful to someone else.

## `clang-omp`

First, the default `clang` does not support OpenMP, so you need a special one:

    brew install clang-omp

## `CMakeLists.txt`
Second, `CMakeLists.txt` needs a few changes:


    set(CMAKE_C_COMPILER clang-omp CACHE STRING "C compiler" FORCE)
    set(CMAKE_CXX_COMPILER clang-omp++ CACHE STRING "C++ compiler" FORCE)
    
    find_package(OpenMP REQUIRED)
    
    set(CMAKE_C_FLAGS "${CMAKE_C_FLAGS} ${OpenMP_C_FLAGS}")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} ${OpenMP_CXX_FLAGS}")
    set(CMAKE_EXE_LINKER_FLAGS "${CMAKE_EXE_LINKER_FLAGS}
    ${OpenMP_EXE_LINKER_FLAGS}")


## `cmake` invocation
Finally, and this was the hardest part to figure out, `cmake` must be run (in a
totally pristine build directory) with the `CC` and `CXX` environment variables
pointing to `clang-omp`:

    $ cd /path/to/build/
    $ rm -rf *
    $ CC=clang-omp CXX=clang-omp++ cmake /path/to/source/
    $ make

## That's it
I'm not certain every line added to `CMakeLists.txt` is necessary, but at least
these steps were sufficient for me.
