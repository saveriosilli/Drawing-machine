# Electronics


We have included a modified and ready to use GRBL for Servo library. To install, first make sure there are no previous installation of any other GRBL libraries in your Arduino libraries folder, then just unzip and copy paste the provided folder in the Arduino Libraries folder.

Restart Arduino software and open the GRBL Upload example in the examples menu, upload the program to your Arduino Uno and the installation is complete.


## Connections


Your Arduino should be equipped with a CNC shield. Make sure the shield has:

1. all 3 jumpers under the drivers for microstepping

2. two jumpers on the Y axis duplication

3. servo motor connected as follow: brown wire \(GND\) to any GND pin on the shield, red wire \(VCC\) to any 5V pin on the shield, orange wire \(signal\) to "Endstop Z-" pin on the shield.

4. 12 Volts and 5 Amps power supply connected to the power supply connector of the CNC shield

5. Stepper motors correctly connected to the 4 pins connector next to the driver \(if motor rotate in the wrong direction, just reverse the connector


## Notes on the servo motor operation

The basic GRBL firmware is normally controlling a _stepper_ motor to move the Z axis. This modified version make use of a _servo_ motor instead to lift the pen up and down. A normal stepper motor is controlled with coordinates coming from the G-code and its movement is expressed in millimetres  or inches. With a stepper motor you can control exactly the linear movement of the Z axis below and above the zero.

​

Using a **servo motor** you can only move the Z axis in two pre-defined positions: _Up \(or above the origin\) and Down \(or below the origin\)_.

​

Using your preferred control software \(Universal G-code Sender, Easel, eCNC to cite a few\) you will have the option to move the Z axis up and down for the length you desire, but with this modified GRBL for Servo firmware you will notice that the servo motor will only move when the machine coordinates actually pass the origin.

​

If your Z axis position is currently at 0mm \(the origin point\) and you move the Z axis up for 5mm, the Z axis new position will be + 5mm, _but your servo motor will not move_.

Likely, if your Z axis position is currently + 5mm and you move the Z axis down for 5mm, the Z axis new position will be 0, _but your servo motor will not move as well._

In both cases, the Z axis position was equal or bigger than zero.

​

On the other hand, if your Z axis position is currently at + 5mm and you move the Z axis down for 10mm, the Z axis new position will be -5mm, _and your servo motor will move once_.

​

**The reason is that the servo motor will only move when the Z axis position passes the origin point.** As long as it passes through the origin you will have your servo motor moving up \(from any point below 0 to any point above 0\) or moving down \(from any point above 0 to any point below 0\).

​

This is very important because you might find yourself clicking the Z axis movement up and down arrow several time without noticing any movement and you might believe it is a hardware problem. Instead, make sure the movements are always crossing above and below the origin point.