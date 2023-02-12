# blinky

### Installing software

To program your microcontroller, you need to install:

- `gdb-multiarch` (on some platforms you may need to use `gdb-arm-none-eabi` instead, make sure to update `.cargo/config` to reflect this change)

Finally, you need to install arm target support for the Rust compiler. To do so, run

```
rustup target install thumbv7m-none-eabi
```



### Serial Flashing

Using a CP2102 (3.3v logic) or another USB-Serial converter, connect its `TX` to pin `A10` and its `RX` to pin `A9`. Also connect 3.3v from the CP2102 to the 3.3v pin on the STM32, and do the same for ground. If you try to power the STM32 from its USB port without this power connection, it won't work.

## Convert to BIN File

`cargo build` will create an ARM ELF file, but we need it in a binary `.bin` format.

### Install the Tools

```
cargo install cargo-binutils
rustup component add llvm-tools-preview
```

### Create the BIN File

```
cargo objcopy --release -- -O binary firmware.bin
```