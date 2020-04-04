---
layout: default
permalink: GetStarted/WindowsCMake
parent: Getting Started
title: Windows with CMake
---

# Getting Started on Windows with CMake
{: .no_toc }

<!--
Notes to those updating this guide:

    * This document should be __simple__ and cover essential items only.
      Notes for optional components should go in separate files.

    * This document parallels getting_started_linux_cmake.md.
      Please keep them in sync.
-->

This guide walks through building the core compiler and runtime parts of IREE
from source. Auxilary components like the Python bindings and Vulkan driver are
documented separately, as they require further setup.

## Prerequisites

### Install CMake

Install CMake version >= 3.13 from https://cmake.org/download/.

> Tip
> {: .label .label-green }
> Your editor of choice likely has plugins for CMake,
> such as the Visual Studio Code
> [CMake Tools](https://github.com/microsoft/vscode-cmake-tools) extension.

### Install Ninja

[Ninja](https://ninja-build.org/) is a fast build system that you can use as a
CMake generator. Download it from the
[releases page](https://github.com/ninja-build/ninja/releases), extract
somewhere, and it to your PATH.

### Install a Compiler

We recommend MSVC from either the full Visual Studio or from "Build Tools For
Visual Studio":

*   Choose either option from the
    [downloads page](https://visualstudio.microsoft.com/downloads/) and during
    installation make sure you include "C++ Build Tools"
*   Initialize MSVC by running `vcvarsall.bat`:

    ```shell
    $ "C:\Program Files (x86)\Microsoft Visual Studio\2019\BuildTools\VC\Auxiliary\Build\vcvars64.bat"
    ```

## Clone and Build

### Clone

Using your shell of choice (such as PowerShell or [cmder](https://cmder.net/)),
clone the repository and initialize its submodules:

```shell
$ git clone https://github.com/google/iree.git
$ cd iree
$ git submodule update --init
```

> Tip
> {: .label .label-green }
> Editors and other programs can also clone the
> repository, just make sure that they initialize the submodules.

### Build

Configure:

```shell
$ cmake -G Ninja -B build\ .
```

> Tip
> {: .label .label-green }
> The root
> [CMakeLists.txt](https://github.com/google/iree/blob/master/CMakeLists.txt) file
> has options for configuring which parts of the project to enable.

Build all targets:

```shell
$ cmake --build build\
```

## What's next?

### Take a Look Around

Check out the contents of the 'tools' build directory:

```shell
$ dir build\iree\tools
$ .\build\iree\tools\iree-translate.exe --help
```

Translate a
[MLIR file](https://github.com/google/iree/blob/master/iree/tools/test/simple.mlir)
and execute a function in the compiled module:

```shell
$ .\build\iree\tools\iree-run-mlir.exe .\iree\tools\test\simple.mlir -input-value="i32=-2" -iree-hal-target-backends=vmla -print-mlir
```

### Further Reading

*   To target GPUs using Vulkan, see
    [Getting Started on Windows with Vulkan](./getting_started_windows_vulkan.md)

More documentation coming soon...

<!-- TODO(scotttodd): Running tests -->
<!-- TODO(scotttodd): Running samples -->
<!-- TODO(scotttodd): "getting_started.md" equivalent for iree-translate etc. -->