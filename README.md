# Remote Control Switch

The circuit is an electronic switch. You can control the whole functionality, change fan speed, turn on or off the lights etc. from your couch or bed using IR remote, Here, I programmed it for 3 types of remote -> 1. Sony TV remote | 2. Chaina TV remote | 3. Small MP3 players remote. VS1838 universal IR receiver is used to receive the infrared signal transmitted by remote control.

## Features

* Phase angle speed control for AC fans with (0-9) 10 steps.
* Two lights can be turn on or off. 
* The LED indicates the status of the IR receiver.
* Remote control with NEC format cheap remote.
* Microcontroller based design with mimimum external components.
* Transformer-less power supply.
* EEPROM options. So, whenever the Main power goes off, the MCU will check the EEPROM data which has the appliances status.

## Hardware

PIC12F675 is a fully functional 8 bit micro controller in eight pin package. The PIC12F family is very similar to microchip popular PIC16F devices and with the same instruction sets. The PIC12F675 is featured with a internal 4 MHz oscillator factory calibrated with in ±1%, six i/o pins and other peripherals like interrupt, timers, ADC module etc.

PIC12F675 and few more components are used to make this project. BT136 is logic level triac from NXP semiconductors® are intended for general purpose bidirectional switching and phase control applications. These devices are designed to directly interfaced with microcontroller or low power gate trigger circuits. The device can be trigger in all four quadrants but it is better to avoid the fourth quadrant which has higher gate trigger and latch currents. This circuit used quadrant two and three to trigger the triac which can handle a load current up to a maximum of 4A.

<p align="center">
  <img src="https://github.com/chayanforyou/Remote-Controlled-Regulator/blob/master/image/triac_quads.gif?raw=true"/>
</p>
<p align="center" >
  <b>
    Figure 2. Definition of operating quadrants of triac (All polarities are referenced with MT1)
  </b>
</p>

The power supply for the circuit is derived from the a 220V, 50Hz ac line using a capacitor (C1) and a zener diodes (ZD1, ZD2). The 5.1V zener diode combined with the forward voltage drop of the rectifier diode produce an IC supply close to 5V. This arrangement is used to drawn a full wave current from the mains supply.


<p align="center">
  <img src="https://github.com/chayanforyou/Remote-Controlled-Regulator/blob/master/image/zero_cross.gif?raw=true"/>
</p>
<p align="center" >
  <b>
    Figure 3. Zero cross detection - PIC12F675 input structure
  </b>
</p>

The zero cross is detected by R2 which is connected to microcontroller input pin (GP4) and ac line. The ESD protection diodes at input pin (GP4) allows this connection without damage. The voltage is clamped between Vdd + 0.7 and Vss – 0.7 Volts for positive and negative half cycles respectively. The “interrupt on change” at this pin is enabled for generating an interrupt at each zero cross. The triac is triggered with different phase angle (phase angle control) to make different fan speeds.

The microcontroller has eeprom which is used save the changed value after every key pressed, so at power up, the microcontroller remembers the last fan speed and light state. While starts the fan, the microcontroller completely turn on the triac for two seconds, and it helps to gain the fan speed rapidly, then it is switched to the selected speed.

<p align="center">
  <img width="600px" height="324px" src="https://github.com/chayanforyou/Remote-Controlled-Regulator/blob/master/image/remote_multi.jpg?raw=true"/>
</p>
<p align="center" >
  <b>
    Figure 4. Multi Remote controller (SONY & NEC Protocol)
  </b>
</p>

## Operational Use

**Sony Remote (SONY)**

**Chaina Remote (NEC)**

**MP3 Remote (NEC)**
* The remote control has a total 21 keys, and the keys “0 to 9” are used to control fan speed where "0" is lower and "9" is higher speed, “Mute” will be turn off the fan, "EQ" will be toggle light 1, "VOL+" will be toggle light 2. The "POWER" key is used to turn on or off the device. The "PLAY/PAUSE" and "NEXT" keys can also used to decrease/increase fan speed respectively.

The LED is lit while it accepts the commands from the remote control. And it remains turn on when device is off.

## Components List

| No. | Name | Label |
| --- | --- | --- |
| 01 | PIC12F675 General purpose 8 bit MCU | U1 |
| 02 | Fuse 230V/1A | F1 |
| 03 | 105J/400V Capacitor | C1 |
| 04 | 1000uF/16V Capacitor | C2 |
| 05 | 104 Ceramic Capacitor | C3, C4 |
| 06 | 103J Polyester Film Capacitor | C5-C7 |
| 07 | 5.1V Zener Diode | ZD1, ZD2 |
| 08 | 1N4007 Diode | D1 |
| 09 | 1M Ohm Resistor | R1 |
| 10 | 10M Ohm Resistor | R2 |
| 11 | 330 Ohm Resistor | R3 |
| 12 | 10K Ohm Resistor | R4-R6 |
| 13 | 1K Ohm Resistor | R7-R12 |
| 14 | C1815 Transistor | Q1-Q3 |
| 15 | Triac BT136 | TR1-TR3 |
| 16 | VS1838 Universal IR Sensor| IR |
| 17 | LED 3mm Any Colour | LED |
| 18 | MP3 Remote Control (NEC) |   |

## Schematic

<p align="center">
  <img width="627px" height="450px" src="https://github.com/chayanforyou/Remote-Controlled-Regulator/blob/master/image/schematic.png?raw=true"/>
</p>
<p align="center" >
  <b>
    Figure 5. The circuit diagram. The fan and lights are connected with FAN, L1 and L2.
  </b>
</p>

#### Since there is no transformer for power-line isolation, the user must be very careful and assess the risks from electric shock hazards. The author is not responsible for any damages arising from any use of this circuit.

## PCB Layout

<p align="center">
  <img width="601px" height="200px" src="https://github.com/chayanforyou/Remote-Controlled-Regulator/blob/master/image/pcb_layout.png?raw=true"/>
</p>
<p align="center" >
  <b>
    Figure 6. Remote control switch PCB with top silk and solder mask layer.
  </b>
</p>

```
The PCB is designed with Adobe Photoshop. The circuit, pcbs and mikroC code for programming PIC12F675 are available in this repository. Please take care not to erase the internal oscillator calibration constant, which is written to the last location program memory. The Microchip® Development Tools maintain all calibration bits to factory settings, or if you are using IC-Prog, it will ask you before erasing.
```

**Note:** The circuit is tested on 220v 50Hz AC line and works perfectly.

## Important Note

*This demonstration code is for learning purpose. It's not so efficient or optimized that you can use it commercially. But is ok for prototype and hobbyist project. If you need optimized code and different IR protocol version for different remote or want to use it commercially contact:- <chayanforyou@yahoo.com>*

## Troubleshooting

If the device does not respond to the remote control signals then look for the following.

1. PIC12F675’s Configuration Register is
   - CONFIG : $2007 : 0x3014
2. Remote Control is NEC Format `Same Model` Only (Chinese MP3 player remote works good, Other Remote does not work)
3. IR sensor is of good quality and must be labeled VS1838 (other values won’t work).

## Contributing

Want to contribute? You are welcome! 
Note that all pull request should go to `dev` branch.

## Developed By

* Chayan Mistry - <chayanforyou@yahoo.com>

### Thanks to

* [Hamradio](http://www.hamradio.in/circuits/fan_regulator.php)
* [Extreme Electronics](http://extremeelectronics.co.in/avr-projects/avr-project-remote-controlled-fan-regulator/)

## License

> Anyone can use and share the code completly free, but keeping the original content unchanged and with enough credit. Commercial use is totally prohibited.

[![](https://github.com/chayanforyou/Remote-Controlled-Regulator/blob/master/image/license.png)](https://creativecommons.org/licenses/by-nc-nd/4.0/)

This work is licensed under a [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License.](https://creativecommons.org/licenses/by-nc-nd/4.0/)

