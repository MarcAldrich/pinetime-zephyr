# PineTime Zephyr

[PineTime](https://www.pine64.org/pinetime/) firmware toolkit based on [Zephyr Project](https://www.zephyrproject.org/) RTOS.

A collection of drivers, libraries and samples to build your own PineTime smart watch firmware.



## Contributing to this project

The pinetime board (watch) has become a part of the zephyr distribution.
This is not the case (yet) for the HR-sensor, touchscreen, accell-sensor.....

The zephyr-included Focaltech touch_controller is usable on the Pinetime (included in samples/display/lvgl).  (minor modification see: drivers/kscan)

## Where To Start?
Read the tutorial! A helpful manual is included in the repository:
 - [pdf](oswatch.pdf)
 - [epub](opensourcewatch.epub)
 - [html](https://najnesnaj.github.io/pinetime-zephyr/html)
 - [md](https://najnesnaj.github.io/pinetime-zephyr/)

## Installation Overview
1. Follow the Zephyr [Getting Started Guide](https://docs.zephyrproject.org/latest/getting_started/index.html) to install zephyr SDK and tools.
2. Install `west` meta tool (https://docs.zephyrproject.org/latest/guides/west/install.html).


build your first sample!

 - west build -p -b pinetime_devkit0 samples/boards/pine64_pinetime


## if you're in for more adventure : 


3. Create a working directory and enter it.
```
mkdir work
cd work
```
3. Use west to clone pinetime repository and initialize pinetime project.
```
west init -m https://github.com/najnesnaj/pinetime-zephyr
```
Alternatively, you can also clone using manifest from specific branch or tag:
```
west init -m https://github.com/<user>/pinetime-zephyr --mr <branch>
```
4. Use `west` to use clone and checkout all dependant repositories specified in `west.yml` (inluding zephyr).
```
west update
```
5. Enjoy!


If you used zephyr and west before and want to stick to the same zephyr copy then you can clone pinetime next to zephyr in working directory and update manifest and west.
```
west config manifest.path pinetime
```

Resources:
- West documentation: https://docs.zephyrproject.org/latest/guides/west
- nRF Connect SDK is using zephyr in similar way and its documentation can be helpful as well: https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/gs_installing.html

## Tips & Tricks

### Logging/Shell/Console

#### Segger RTT (Real Time Transfer)
Pinetime does not have UART pins but UART-like connection can be achieved using RTT (Real Time Transfer)
feature of Segger JLink debugger. RTT data can be accessed using SEGGER tool (RTTViewer) or by using
telnet connection to active debug session. Second methond is recommended since it gives better throughput
and allows bitdirection communication using Zephyr Shell (with RTT as backend). PuTTY can be used to
telnet to debug session.

Prerequisites:
- JLink debugger, for example one of Nordic Semiconductor Development Kits.
- Setup: https://wiki.pine64.org/index.php/PineTime#Using_JLink_programmer_and_nrfjprog_tools

Following steps needs to be taken to run RTT shell in the application:
1. Install PuTTY and Setup RTT session. On Linux, copy `misc/rtt_shell/rtt` to `~/putty/sessions`. On Windows,
execute `misc/rtt_shell/putty-rtt.reg`.
2. Enable logging and shell over RTT:
```
CONFIG_LOG=y
CONFIG_USE_SEGGER_RTT=y
CONFIG_SHELL=y
CONFIG_SHELL_BACKEND_RTT=y
```

3. Build and flash application.

4. Start debug session
```
west debug (will start gdb)
continue (in gdb console)
```
5. Start PuTTY RTT session, prompt should be printed.

Resources:
- Zephyr shell documentation: https://docs.zephyrproject.org/latest/reference/shell/index.html
- Zephyr logger documentation: https://docs.zephyrproject.org/latest/reference/logging/index.html

## What Is Included?
In this repository you can find files that supplement a zephyr installation.

* **board definition** Contains the board definition for the pinetime.
* **drivers** Contains the drivers for the pinetime.
* **samples** Modified samples for blinky, new samples for the ST7789V display etc.

## Project Roadmap
### DONE
- the display
- bluetooth BLE
- graphics libraries
- - LittlevGL
- - Adafruit GFX
- RTC
- Serial NOR flash
- accel sensor
- heart rate sensor
- touchscreen
- CTS (setting time in bluetooth)
- DFU (wireless firmware update)

### TODO
- HR detection (algorithm)
- build-in features of bosch accel sensor (eg step counter)
- testing interrupt/semaphore mechanism on accel sensor and touchscreen
- powermanagement
- watchdog


#### Other watches 

There are quite a few hackable watches, based on the same nrf52832 microcontroller.
I have also made a repository for the desay D6, which is a ssd1306 OLED based, cheap chinese watch with a serial port.
[other smartwatches](https://github.com/najnesnaj/dsd6-zephyr)
This watch combined with a "blue-pill" black magic debug probe, which contains a serial port, might be one of the cheapest zephyr dev boards available!


