# test_dynamoDIO

## Install

1. Check [here](https://dynamorio.org/page_releases.html)
1. Unzip the file to a folder.
1. Create an alias for the command:
```bash
alias drrun=/your/path/to/DynamoRIO/bin/drrun
```

## Tracing Instructions
1. Under the folder `samples` and they are source code `instrace_simple.c` and `instrace_x86.c`. Their binaries are under the folders `bin32` and `bin64`.
1. To trace a compiled binary, one can use the command like:
```bash
drrun -c /path/to/instrace_x86.so -- compiled_binary
```
1. Once it is done, one can find the log instructions in a log file under the same folder as the binary.

Note: the `.so` files are in the folder `~/Apps/DynamoRIO-Linux-11.3.0-1/samples/bin64`.

## Build DynamoRIO Dummy Client
1. Create a folder where the source files are located (Here we use `test_client` as an example).
1. Go to the `test_client` folder
1. In the `.c` file, import the following header:
```c
#include "dr_api.h"
```
1. Create the `CMakeLists.txt` in the folder.
1. Put the following content in the cmake file:
```make
## These two lines are must otw cmake will complaint.
cmake_minimum_required(VERSION 3.7)
project(TestMyDummyClinet)

add_library(test_client SHARED test_client.c)
find_package(DynamoRIO)
if (NOT DynamoRIO_FOUND)
  message(FATAL_ERROR "DynamoRIO package required to build")
endif(NOT DynamoRIO_FOUND)
configure_DynamoRIO_client(test_client)
```
1. Run `cd ..` and `make`:
```bash
## Import the predefined cmake file will save us a lot of time!
cmake -DDynamoRIO_DIR=$DYNAMORIO_HOME/cmake test_client
make
```
1. After make, we will see a file call `libtest_client.so` and we can use it with `drrun` command like:
```bash
drrun -c libtest_client.so -- <test_binary>
```

Reference: https://dynamorio.org/page_build_client.html