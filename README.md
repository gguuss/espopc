# espopc
(ESP32 fork of) Open Pixel Control protocol for WS281x LEDs

ESPOPC is similar to a Fadecandy controller with Fadecandy server with a WiFi
interface. Adding a battery makes the LED array + ESP8266 combination portable.

## System overview

```
 PC running      -> WiFi -> ESP32 -> 3.3V -> 5V -> NeoPixel
 grid8x8_dot.pde                                     8x8 array
```

- Drives one WS281x LED strip up to 1024 LEDs but only tested up to 128 LEDs arranged in an 8x16 grid.
- Implements the Open Pixel Control protocol on TCP port 7890. This is the same protocol used by fadecandy server (fcserver).

This is not a Fadecandy controller hardware clone.

- No dithering.
- No keyframe interpolation.
- Fixed gamma correction of 2.2
- SysEx ignored.

## Compiling

- Build with the ESP8266 board package 1.6.5 or newer.
- ESP8266 CPU Frequency must be set to 160 MHz.
- Use the latest NeoPixelBus library installed using the IDE library manager. The UartDriven branch is no longer supported.
- Connect ESP8266 GPIO2 to the WS281x Data In pin. No other GPIO pin can be used.

The most recent testing was done using Arduino IDE 1.6.7, ESP8266 board package 2.1.0, NeoPixelBus library 2.0.2, and Adafruit Huzzah ESP8266.

## Example programs to drive the LEDs

Many open pixel control and Fade Candy examples work with ESPOPC. Be sure to
modify the examples with the ESP IP address.

The following examples from https://github.com/zestyping/openpixelcontrol work
with ESPOSC.

    python\_clients/
        lava_lamp.py,miami.py,nyan_cat.py,sailor_moon.py,spatial_stripes.py

```
$ ./lava\_lamp.py -l grid8x8.json -s <ESP IP addr>:7890 -f 20
```

The Fadecandy grid8x8 Processing examples at https://github.com/scanlime/fadecandy work with ESPOSC. These examples show how
to create interactive LED displays. Edit the PDE file to add the ESP IP address.

    examples/processing/
        grid8x8_dot, grid8x8_noise_sample, grid8x8_orbits, grid8x8_wavefronts

![Automated Playback](./espopc.gif "Automated Playback")

## References

The NeoPixelBus library is used to drive the WS281x LEDs. The UartDrive method
has been merged into the master release branch so the UartDriven branch should
no longer be used. This change also requires the WS281x Data In pin be
connected to ESP8266 GPIO2.

See https://github.com/Makuna/NeoPixelBus for more details.

See https://github.com/zestyping/openpixelcontrol for the OPC protocol specification.

This Adafruit LED art tutorial covers wiring and powering the LEDs, etc. In
addition, it covers installing and running Fadecandy example programs.

https://learn.adafruit.com/led-art-with-fadecandy/
