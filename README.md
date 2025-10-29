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
