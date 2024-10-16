# Fibonacci: A template project for Valida

This is a simple program that calculates the n-th fibonacci number.

To run it in the Valida VM, you need the Valida toolchain installed. Follow the instructions [here](https://github.com/lita-xyz/valida-toolchain/blob/main/README.md).

Then, build the project, in the parent folder `fibonacci`:

```
CC_delendum_unknown_baremetal_gnu=/valida-toolchain/bin/clang CFLAGS_delendum_unknown_baremetal_gnu="--sysroot=/valida-toolchain/ -isystem /valida-toolchain/include" RUSTFLAGS="-C linker=/valida-toolchain/bin/ld.lld -C link-args=/valida-toolchain/DelendumEntryPoint.o -C link-args=--script=/valida-toolchain/valida.ld -C link-args=/valida-toolchain/lib/delendum-unknown-baremetal-gnu/libc.a -C link-args=/valida-toolchain/lib/delendum-unknown-baremetal-gnu/libm.a -C link-args=--noinhibit-exec" cargo +delendum build --target=delendum-unknown-baremetal-gnu --verbose
```

To run it in the Valida VM, run the built binary in either `Valida-shell` or the Valida binary:

In Valida-shell:

```
valida>valida run ~/fibonacci/target/delendum-unknown-baremetal-gnu/debug/fibonacci log 25.bin
```

The file 25.bin is a binary file containing the number 25. It can be created with:

```
echo -ne '\x19' > 25.bin
```

This is the input to the `fibonacci` program.

The `run` command will load the binary, and execute the program. The program will then run, and print the output to the console and the file `log` in the current directory.

The log file should contain:

```
25
-th fibonacci number is:
75025
```