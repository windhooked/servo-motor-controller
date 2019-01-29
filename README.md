This work is based on the DC Servomotor Controller by Elm Chan:
http://elm-chan.org/works/smc/report_e.html

## Files in this repository

The original archives are unpacked into chan/smc and chan/smc3.

chan/smc/smc.asm: v0.2 of the motor controller (AT90S2313)

chan/smc/smc2.asm: v0.2 of the motor controller with position display on a
7-segment display connected via SPI to the ISP connector. (AT90S2313)

chan/smc3/SMC3.ASM: v0.3, ATtiny2313. Supports serial interface, but not the
stepper-like dir/step input and no LED display.

chan/smc3/SMC3A.ASM: v0.3a, ATtiny2313. Supports the stepper-like dir/step
interface, but no serial interface and no LED display.


## Compiling

Chan wrote his files for the orignal AVR assembler. The open source
alternative [avra](http://avra.sourceforge.net/) can be used as well:

	avra -I /usr/share/avra smc3.asm



## Features of SMC3

 o Using Only a Cheap ATtiny2313 Microcontroller
 o Controlled in Serial Command via UART
   - Direct Access to Position Command Register
   - G0/G1 Motion Generation
 o Three Control Modes
   - Absolute Positioning Mode
   - Constant Speed Mode
   - Constant Torque Mode
 o Software Decoding of Quadrature Encoder Input
   - Count rate over 100,000 counts/sec in quadrature decoding
   - No External Component Required
 o Two PWM Outputs for H-bridge Driver
 o Three Diagnostic Outputs
   - Ready, Torque Limit and Servo Error
 o On-the-Fly Servo Tuning

Changes from SMC to SMC3

 o Removed Pulsed Input
 o Added Diagnostic Outputs
   - Ready: Servo control is running.
   - Torque Limit: Torque limit indicator for mode 2/3.
   - Servo Error: Servo error occured and enterd to mode 0. M command or
     reset can restart servo.


## Features of SMC3A

 o Using Only a Cheap ATtiny2313 Microcontroller
 o Optimized for Replacement of Stepping Motors
   - Pulse/Dir Command Input with Pulse Multiplyer
   - Pulse rate over 100,000 pulses/sec
   - Gear ratio from 1/256 to 255 in 1/256 step
 o Three Control Modes
   - Relative Positioning Mode
   - Constant Speed Mode
   - Constant Torque Mode
 o Software Decoding of Quadrature Encoder Input
   - Count rate over 100,000 counts/sec in quadrature decoding
   - No External Component is Required
 o Two PWM Outputs for H-bridge Driver
 o Three Diagnostic Outputs
   - Ready, Torque Limit and Servo Error
 o On-the-Fly Servo Tuning


Changes from SMC to SMC3A

 o Removed G0/G1 Commands
 o Added +/- Commands
   - {+|-}<value>: Increase/Decrease command counter.
 o Extened Pulsed Input Function
   - Pulse Multiplyer: Gear ratio (8.8 fixed-point) can be set with parameter
     #6, 256 means 1.0. Parameter #7 has no effect.
 o Added Diagnostic Outputs
   - Ready: Servo control is running.
   - Torque Limit: Torque limit indicator for mode 2/3.
   - Servo Error: Servo error occured and enterd to mode 0. M command or
     reset can restart servo.
 



## CPU

The AT90S2313 got replaced by the ATtiny2313 a long time ago. They are very
similar, only some register names changed slightly and the interrupt table
got a little bigger. See Atmel/Microchip AVR091 for details on migration.

Today I would choose one of these AVR CPUs (based on price and
availability):

- ATtiny25: cheapest AVR today, but QFN only
- ATtiny44: SO14, 4kB flash, only slightly more expensive
- ATtiny45: SO20


## Further reading

[ATtiny2313 data sheet](http://ww1.microchip.com/downloads/en/DeviceDoc/doc8246.pdf)

AVR091 Replacing AT90S2313 by ATtiny2313.pdf
