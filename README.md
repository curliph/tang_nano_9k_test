## LiteX test for tang\_nano\_9k under Windows Powershell/WSL

Before patch merged to main stream, you can run test by replace <br>
files inside patch directory to corresponding files inside LiteX.

Test run with oss-cad-suite (https://github.com/yosyshq/oss-cad-suite-build):

## Step Guide

1. download and install [Gowin IDE](https://www.gowinsemi.com) (Education Version is also okay)
2. download and install [oss-cad-suite](https://github.com/YosysHQ/oss-cad-suite-build/releases)
3. download and install [riscv toolchain](https://static.dev.sifive.com/dev-tools/riscv64-unknown-elf-gcc-8.3.0-2020.04.1-x86_64-w64-mingw32.zip)
4. setup risc-v toolchain path to system environments
5. setup Gowin IDE/Programmer binary directory to system environments
6. download [litex_setup.py](https://raw.githubusercontent.com/enjoy-digital/litex/master/litex_setup.py)
7. start oss-cad-suite box by running 'start.bat' inside its directory

```
# follow steps run inside oss-cad-suite box

[OSS CAD Suite] > mkdir enjoy-digital
[OSS CAD Suite] > cd enjoy-digital
[OSS CAD Suite] > cp ../litex_setup.py . 
[OSS CAD Suite] > python3 litex_setup.py --init --install --config=full

[OSS CAD Suite] > pip3 install meson ninja
 
[OSS CAD Suite] > git clone https://github.com/curliph/tang_nano_9k_test 
[OSS CAD Suite] > cd tang_nano_9k_test

[OSS CAD Suite] > cp patch/litex/programmer.py ../enjoy-digital/litex/litex/build/gowin 
[OSS CAD Suite] > cp patch/litex/gowin.py ../enjoy-digital/litex/litex/build/gowin 
[OSS CAD Suite] > cp patch/litex-boards/platforms/*.py ../enjoy-digital/litex-boards/litex-boards/platforms 
[OSS CAD Suite] > cp patch/litex-boards/targets/*.py ../enjoy-digital/litex-boards/litex-boards/targets 
```

### for programming with Gowin Programmer
```
[OSS CAD Suite] > python3 test.py --build --load --prog-kit gowin # load to internel sram
[OSS CAD Suite] > python3 test.py --build --flash --prog-kit gowin # flash bitstream to internel embFLASH
```

### for programming with openFPGALoader
1. download [zadig](https://zadig.akeo.ie)
2. connect tang-nano-9k to computer, replace its [JTAG Debugger (interface 0)] with WinUSB driver by zadig

```
[OSS CAD Suite] > python3 test.py --build --load  # load to internel sram 
[OSS CAD Suite] > python3 test.py --build --flash  # flash bitstream to embFLASH and bios to external SPINAND
``` 
