---
description: >-
  Python c++ extension modules made with pybind11 can be debugged right from the
  CLion editor.
---

# Debugging pybind11 modules with CLion

Original article is here: [http://unixnme.blogspot.com/2019/11/debug-pybind11-c-extension-with-clion.html](http://unixnme.blogspot.com/2019/11/debug-pybind11-c-extension-with-clion.html)

To debug the C++ extension with CLion you can use the following CMake configuration:

```text
# CMakeLists.txt
cmake_minimum_required(VERSION 3.17)
project(your_project)

set(CMAKE_CXX_STANDARD 14)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY your_output_dir)
set(PYTHON_EXECUTABLE /path/to/your/python)
set(CMAKE_BUILD_TYPE Debug)

# Your project needs to have this dir available (clone from GitHub)
add_subdirectory(pybind11)

# See pybind docs for main.cpp
pybind11_add_module(your_ext_name src/main.cpp)

target_compile_definitions(your_ext_name PRIVATE)

```

The `pybind11` repository can be found from `https://github.com/pybind/pybind11` . Make it available under a folder `pybind11`. 

#### Debugging with CLion

The above `CMakeLists.txt` defines a CMake target called `your_ext_name` .

Choose "Run" -&gt; "Edit Configurations" and either modify or create a new "CMake Application" configuration for the target:

* **Target**: `your_ext_name`
* **Executable**: `/path/to/your/python`
* **Program arguments**: `python_script_to_run.py`
* **Working directory**: `/path/to/your/repository`
* **Environment variables**: `PYTHONPATH=/path/to/repository/cmake-build-debug`

The `PYTHONPATH` environment variable above enables finding the Python package built with CMake instead of `setup.py`.

Now you should be able to set breakpoints and debug from the IDE.

