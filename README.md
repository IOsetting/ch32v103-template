# About 

WCH CH32V103 project template for CLi and VSCode

# File Structure

```
CH32V103C-TEMPLATE
├── Build                        # Build results
├── Core                         # RISC core
├── Debug                        # Delay and UART methods for debug
├── Ld                           # LD file
├── Makefile
├── Peripheral                   # Peripheral libraries
├── Startup                      # ch32v10x startup file
├── User                         # User application code
└── Util                         # OpenOCD config file
```

# How To Use

## Hardware

* CH32V103x  
  CH32V103C8T6 Bluepill or any CH32V10x EVB
* WCH-Link  
  Qinheng ARM/RISC-V MCU programmer and debugger

## Install Toolchains

Download toolchains from [http://mounriver.com/download](http://mounriver.com/download), switch to Linux tab and look for the file named *MRS_Toolchain_Linux_x64_Vx.xx.tar.xz*, toolchains file structure
```
── beforeinstall
│     ├── 50-wch.rules
│     ├── 60-openocd.rules
│     ├── libhidapi-hidraw.so -> libhidapi-hidraw.so.0.0.0
│     ├── ...
│     ├── libusb-1.0.so.0.3.0
│     └── start.sh
├── OpenOCD
│     ├── bin
│     │     ├── openocd
│     │     ├── wch-arm.cfg
│     │     └── wch-riscv.cfg
│     └── share
├── README
└── RISC-V Embedded GCC
    ├── bin
    ├── distro-info
    ├── include
    ├── lib
    ├── lib64
    ├── libexec
    ├── riscv-none-embed
    └── share
```
**RISC-V Embedded GCC**  
Standard RISC-V gcc, you can replace it with a newer version from [https://github.com/xpack-dev-tools/riscv-none-embed-gcc-xpack/releases](https://github.com/xpack-dev-tools/riscv-none-embed-gcc-xpack/releases). Extract it to /opt/gcc-riscv

**OpenOCD**  
A customized OpenOCD for WCH-Link, Extract it to /opt/openocd

## UDEV Rules and Libs

Run *start.sh* under beforeinstall, or manually setup the udev rules and the dynamic lib files. You can run the following command with EVB and WCH-Link connected
```bash
./openocd -f wch-riscv.cfg -c init -c halt
```
if everything goes correctly
```
...
Info : WCH-Link-CH549  mod:RV version 2.5 
Info : wlink_init ok
Info : This adapter doesn't support configurable speed
Info : JTAG tap: riscv.cpu tap/device found: 0x00000001 (mfg: 0x000 (<invalid>), part: 0x0000, ver: 0x0)
Warn : Bypassing JTAG setup events due to errors
Info : [riscv.cpu.0] datacount=2 progbufsize=8
Info : Examined RISC-V core; found 1 harts
Info :  hart 0: XLEN=32, misa=0x0
[riscv.cpu.0] Target successfully examined.
...
```

## Build And Download

Checkout this project
```bash
git clone https://github.com/IOsetting/ch32v103-template
```
Edit Makefile, update the paths
```
TOOL_CHAIN_PATH ?= /opt/gcc-riscv/riscv-none-embed-gcc-10.2.0-1.2/bin
OPENOCD_PATH    ?= /opt/openocd/wch-openocd/bin
```
Then make
```bash
# clean
make clean
# make
make
# download
make flash
```
If everything goes correctly, you will see the C13 LED blinking.

# License

Copyright (c) 2022-present IOsetting iosetting@outlook.com

This project is licensed under the permissive Apache 2.0 license, you can use it in both commercial and personal projects with confidence.
