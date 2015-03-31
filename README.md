SCI-Solver_FEM
==============

SCI-Solver_FEM is a C++/CUDA library written to solve an FEM linear system. It is designed to solve the FEM system quickly by using GPU hardware.

The code was written by Zhisong Fu and T. James Lewis. The theory behind this code is published in the paper:
"Architecting the Finite Element Method Pipeline for the GPU"

**AUTHORS** Zhisong Fu(a,b), T. James Lewis(a,b), Robert M. Kirby(a,b), Ross T. Whitaker(a,b)

`  `a-School of Computing, University of Utah, Salt Lake City, UT, USA

`  `b-Scientific Computing and Imaging Institute, University of Utah, Salt Lake City, USA

**ABSTRACT**
The finite element method (FEM) is a widely employed numerical technique
for approximating the solution of partial differential equations (PDEs) in var-
ious science and engineering applications. Many of these applications benefit
from fast execution of the FEM pipeline. One way to accelerate the FEM
pipeline is by exploiting advances in modern computational hardware, such as
the many-core streaming processors like the graphical processing unit (GPU).
In this paper, we present the algorithms and data-structures necessary to move
the entire FEM pipeline to the GPU. First we propose an efficient GPU-based
algorithm to generate local element information and to assemble the global lin-
ear system associated with the FEM discretization of an elliptic PDE. To solve
the corresponding linear system efficiently on the GPU, we implement a conju-
gate gradient method preconditioned with a geometry-informed algebraic multi-
grid (AMG) method preconditioner. We propose a new fine-grained parallelism
strategy, a corresponding multigrid cycling stage and efficient data mapping
to the many-core architecture of GPU. Comparison of our on-GPU assembly
versus a traditional serial implementation on the CPU achieves up to an 87×
speedup. Focusing on the linear system solver alone, we achieve a speedup of
up to 51× versus use of a comparable state-of-the-art serial CPU linear system
solver. Furthermore, the method compares favorably with other GPU-based,
sparse, linear solvers.

Requirements
==============

 * You will need a CUDA Compatible Graphics card. See <a href="https://developer.nvidia.com/cuda-gpus">here</a>.
 * SCI-Solver_FEM is compatible with the latest CUDA toolkit (7.0). Download <a href="https://developer.nvidia.com/cuda-downloads">here</a>.
 * This project has been tested on OpenSuse 12.3 (Dartmouth) on NVidia GeForce GTX 570 HD, Windows 7 on NVidia GeForce GTX 775M, and OSX 10.10 on NVidia GeForce GTX 775M. 
 * If you have a CUDA compatible card with the above operating systems, and are experiencing issues, please contact the repository owners.
 * Windows: You will need Microsoft Visual Studio 2013 build tools. This document describes the "NMake" process.

Building
==============
Instructions for building the library:

<h3>Unix</h3>
```c++
cd SCI-SOLVER_FEM/build
cmake ../src
make
```

**Note:** You may need to specify your CUDA toolkit location:
```c++
cmake -DCUDA_TOOLKIT_ROOT_DIR="/usr/local/cuda" ../src
make
```
(Assuming this is the location).

<h3>Windows</h3>
Open a Visual Studio (32 or 64 bit) Native Tools Command Prompt. 
Follow these commands:
```c++
cd C:\Path\To\SCI-Solver_FEM\build
cmake -G "NMake Makefiles" ..\src
nmake
```

<h3>OSX</h3>
```c++
cd SCI-SOLVER_FEM/build
cmake ../src
make
```

If you have compile errors such as <code>undefined reference: atomicAdd</code>, it is likely you need to set your compute capability manually. A known capability is 2.0.

```c++
cmake -DCUDA_COMPUTE_CAPABILITY=20 ../src
make
```

Running Examples
==============

You will need to enable examples in your build to compile and run them

```c++
cmake -DBUILD_FEM_SOLVER_EXAMPLES=ON ../src
make
```

You will find the example binaries built in the <code>build/examples</code> directory.

Run the examples in the build directory:

```c++
examples/Example1
examples/Example2
...
```

Follow the example source code in <code>src/examples</code> to learn how to use the library.

Using the Library
==============

A basic usage of the library links to the <code>libFEM_CORE</code> library during build and 
includes the headers needed, which are usually no more than:

```c++
#include "setup_solver.h"
#include "cuda_resources.h"
```

Then a program would setup the FEM parameters using the 
<code>AMG_Config</code> object and call <code>setup_solver()</code> to generate
the answer matrices.

You will need to make sure your CMake/Makfile/Build setup knows where to point for the library and header files. See the examples and their CMakeLists.txt.
