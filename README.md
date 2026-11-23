# SIGNALDuino uC v4.2.3 (development version) for Maple Mini and ESP32 with multi cc1101 and xFSK support

> **Branch `maple-bluepill-pycul`** - a few small patches on top of
> `dev-r423_cc1101` so the firmware also speaks the **culfw "moritz" serial
> dialect** and can serve as a **NanoCUL replacement for EQ3 MAX!** (e.g. with
> [PyCUL](https://github.com) / Home Assistant or FHEM's `14_CUL_MAX.pm`) on an
> STM32F103 Blue Pill with one CC1101 (868 MHz) on radio A:
>
> 1. **`BLUEPILL_LED` build flag** - activity LED on the Blue Pill's onboard
>    LED (PC13, active low); without the flag nothing changes.
> 2. **NanoCUL/culfw compatibility for MAX!** - `X`/`X21` answer
>    `<flags> <credit10ms>` with culfw's duty-cycle credit (max 900, +1/s,
>    `LOVF` when exhausted), `Zr`, `Zw<6hex>` (fake wall thermostat address,
>    persisted in EEPROM), `LENERR`, and received frames are additionally
>    printed as `Z<hex>` (+ RSSI byte when `X21` is set). The usual
>    `MN;D=` output stays untouched, so the normal FHEM SIGNALduino path
>    keeps working.
> 3. **Command burst fix** - commands arriving back-to-back in one USB write
>    were merged and lost in `serialEvent()`; culfw-style clients write init
>    sequences and `Zs..`+`X` pairs without pauses and need this.
>
> Build for the Blue Pill (USB serial, one CC1101 on radio A):
> `PLATFORMIO_BUILD_FLAGS="-DBLUEPILL_LED=1" pio run -e Maple_sduino_USB`.
> Prebuilt images: see this fork's releases. Wiring, bootloader and setup
> documentation is kept in a companion repository (`maple-signalduino`).

### Getting started

System to receive digital signals and provide them to other systems for demodulation.

Firmware files  are in https://github.com/Ralf9/SIGNALDuino/releases

Compile it or use the and have fun.  
- If you are using the Arduino IDE, you have to copy the folder "SIGNALduinoAdv" with its contents into your sketch folder and edit the file compile_config.h 
 - If you use LAN, you need the Ethernet Library
 - If you use the ESP32, you need the WifiManager by tablatronix/tzapu
- If you are using platformio, you have to copy the files "extra_script.py", "platformio.ini" and the folder "SIGNALduinoAdv" with its contents into your project folder. 

### Using SIGNALDuino in FHEM

If you want to use the SIGNALDuino with FHEM, you can use it directly from FHEM. No need to compile any sourecode.
You find more Information here: https://wiki.fhem.de/wiki/Maple-SignalDuino  
https://forum.fhem.de/index.php/topic,106278.0.html

### Tested microcontrollers

* STM32 F103CBT6 (Maple Mini, bootloader v2.0)
* ESP32 (DEVKIT V1, D1 mini) 

### Signal from my device ist not detected

We have a pattern detection engine, that detect serval signal types. May not all, but most of them.

