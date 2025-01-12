# Blink example for Pico-W

Example code from the <https://github.com/soypat/cyw43439> module.

The Pico-W LED is connected to the WiFi module so the plain old
Pico examples won't work.

I am using the Raspberry Pi Debug Probe
<https://www.raspberrypi.com/documentation/microcontrollers/debug-probe.html#the-debug-probe>
So the build/flash commands below are to suit that.

## Requirements

I am using [Bluefin](https://docs.projectbluefin.io/) DX, a Fedora based distribution, and
have the following packages over those provided by default:

### Fedora packages

- gdb
- hidapi
- openocd

### VS Code extensions

- Go
- TinyGo
- Serial Monitor
- Markdown All in One
- markdownlint

## Building

Using `-serial=uart` causes the standard output to go via the UART rather than USB.

```sh
tinygo build -target=pico-w -serial=uart blink.go
```

### Flashing

Using [OpenOCD](https://openocd.org/) to flash a previously built ELF file.

```sh
openocd -f interface/cmsis-dap.cfg -f target/rp2040.cfg -c "adapter speed 5000; program blink.elf verify reset exit"
```

Using TinyGo to build and flash (which uses openocd).

```sh
tinygo flash -target=pico-w -serial=uart -programmer=cmsis-dap -ocd-commands "adapter speed 5000;" blinky.go
```
