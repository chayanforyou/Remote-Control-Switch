# Remote Controlled Regulator

The circuit is an electronic fan regulator based on Interrupt and Timmer. You can control the whole functionality, change fan speed, turn on or off the lights etc. from your couch or bed using cheap NEC Format remote, usually supplied with small MP3 players. VS1838 universal IR receiver is used to receive the infrared signal transmitted by remote control.

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

The power supply for the circuit is derived from the a 230V, 50Hz ac line using a capacitor (C1) and a zener diodes (ZD1, ZD2). The 5.1V zener diode combined with the forward voltage drop of the rectifier diode produce an IC supply close to 5V. This arrangement is used to drawn a full wave current from the mains supply.


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
  <img width="203px" height="400px" src="https://github.com/chayanforyou/Remote-Controlled-Regulator/blob/master/image/remote_normal.jpg?raw=true"/>
</p>
<p align="center" >
  <b>
    Figure 4. Remote controller (actual size 85 x 39 x 6 mm)
  </b>
</p>

## Operational Use

The remote control has a total 21 keys, and the keys “U/SD to 9” are used to control fan speed where "U/SD" is lower and "9" is higher speed, “Mute” will be turn off the fan, "EQ" will be toggle light 1, "VOL+" will be toggle light 2. The "POWER" key is used to turn on or off the device. The "PLAY/PAUSE" and "NEXT" keys can also used to decrease/increase fan speed respectively.

The LED is lit while it accepts the commands from the remote control. And it remains turn on when device is off.

## Contributing
Want to contribute? You are welcome! 
Note that all pull request should go to `dev` branch.

## Developed By

* Chayan Mistry - <chayan@cruxlab.xyz>

### Thanks to

* [Hamradio](http://www.hamradio.in/circuits/fan_regulator.php)
* [Extreme Electronics](http://extremeelectronics.co.in/avr-projects/avr-project-remote-controlled-fan-regulator/)

## License

![](https://github.com/chayanforyou/Remote-Controlled-Regulator/blob/master/image/license.png?raw=true)

Anyone can use and share the code completly free, but keeping the original content unchanged and with enough credit. Commercial use is totally prohibited.

This work is licensed under a [Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License.](https://creativecommons.org/licenses/by-nc-nd/4.0/)

