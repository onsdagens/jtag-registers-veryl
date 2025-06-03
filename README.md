# JTAG Registers Veryl

Part of a Veryl interpretation of the JTAG specification. This repo implements a generic instruction register and data registers, following the JTAG spec. 

An minimal synthesizeable example using [`tap-controller-veryl`](https://github.com/onsdagens/tap-controller-veryl) is provided in `./src/fpga_top.veryl`.

The provided build scripts and constraints target the Numato Lab ECP-5 FPGA Development Board, but the example should be generizable by changing them to match your specific FPGA and board. The rest of this readme concerns itself with the FPGA example.
## Dependencies

The toolchain consists of:

- [Veryl](https://veryl-lang.org/install/) for transpiling Veryl code to SystemVerilog.
- [Yosys](https://github.com/YosysHQ/yosys?tab=readme-ov-file#building-from-source) for synthesis
- [Slang](https://github.com/MikePopoloski/slang) SystemVerilog frontend for Yosys.
- [NextPNR](https://github.com/YosysHQ/nextpnr?tab=readme-ov-file#getting-started) for place and route
- [OpenOCD](https://openocd.org/pages/getting-openocd.html) for programming the device
- [Project Trellis](https://github.com/YosysHQ/prjtrellis) for bitstream generation, and other device specifics
- [ftdaye](https://github.com/onsdagens/ftdaye/) for interacting with the JTAG module from the host machine.
## Building and programming

With the toolchain set up, and the dev board connected, run 
```
make
```
to build the project and reprogram the FPGA. 

## Expected behavior

The FPGA example implements a standard `IDCODE` register returning `0xDEADBEEF`. Additionally, a custom 4-bit data register is provided at address `0b0001`. The current content of the register is displayed using the green LEDs as a bit display.

For low level communication with the JTAG module from a host device, we have been using the [ftdaye `ECP5` example](https://github.com/onsdagens/ftdaye/blob/master/examples/ECP5.rs). It contains minimal examples of manipulating the state machine, and reading from and writing to registers.
