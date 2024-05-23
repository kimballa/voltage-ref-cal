
Voltage reference calibration tool
==================================

Precision referenced voltages in 1.000V increments for calibration
of exponential converters in VCOs, VCFs, etc. 

Also usable as a manual GATE/TRIGGER signal generator.

Operation
---------

The rotary switch selects the "baseline voltage" for the output (mono jack J3 and dupont
pins J4), and can set the baseline to between 0 and 5V in 1V increments. 

When pressed, the buttons add further voltages to this; setting the baseline to 4V and
pressing the 2V button will cause the output to jump to 6V. Pressing multiple buttons
at once will sum them up; pressing the 2V and 1V buttons will add 3V to the baseline
as sent to the output, etc. 

The **REF IN** input (J1) takes a voltage input and buffers it; this voltage will be
added to the output when the +IN button is pressed. This reference input voltage can be
any voltage between the power rails, including negative voltages down to -12V.

This device is powered by +/-12VDC input via the Molex MicroFit 3.0 connector J2.  Setting
the power rails at up to +/-18V is acceptable; above this voltage level, the Zener diodes
will exceed power dissipation ratings.  The opamp will also tolerate this level just fine.

Calibration
-----------

Before use, adjust trimpots RV1 and RV2 as follows:

* Set baseline to 5V.
* Give circuit ~60 seconds to warm up.
* Measure output voltage with a DMM.
* Adjust RV1 until output (or test point TP4) reads 5.000V.
* Set baseline to 0V.
* While holding down the +5V button, adjust RV2 until output voltage reads 5.000V.
  (Or measure with DMM at test point TP5 without needing to press the +5V button.) 

Usage tips
----------

### VCO calibration

The primary purpose of the device is to assist in calibration of exponential converters
for VCOs, VCFs, or similar audio equipment. Calibration of this equipment is typically to
establish a 1V / Octave frequency response. Use the knob to set the baseline voltage
at the root of a given octave, and press the +1V button to change the output to the next
octave up in a step-function fashion. This output voltage should be fed as the CV to
the VCO.

An oscilloscope connected to the output of the VCO will show the output waveform. If the
1V/Oct response is maintained, pressing the +1V button will double the frequency and (half
of) the zeroes of the double-frequency waveform will be in the exact same position as the
zeroes of the root-frequency waveform.

Increasing the baseline voltage with the knob allows you to test this 1V / 1 octave step
response throughout the range of the DUT. To test beyond the 6th octave, set the baseline
voltage to 4V and hold down the +2V button to set the baseline at 6V, then press the +1V
button to test the 7V response, etc.


### As standalone GATE / Trigger

To test other functionality of a device that requires a GATE or trigger input, set
the baseline to 0V and press the +5V button to send a GATE signal to the DUT. The +3V
button can be used to trigger devices with a 3.3V logic input. 


Misc
----

Output can be taken from the mono jack or from the pins on connector J4. Both pins of
J4 are the same, and allow easy connection via jumper to breadboard, etc., or connection
of hook-style oscilloscope or DMM probes directly to this board. Matching ground
connection pins are available on J5. 

The output sum will top out at approximately +11.75V (possibly as low as +11V if the
output is used to drive a 2kΩ load). 

If no input is provided to the REF IN jack, it is normaled to ground (+IN button will add
0V to the output).

The rotary switch is a 1-pole, 6-position switch, Alpha MPN `SR1712F-0106-20F0A-N9-N-027`.
This device is now marked obsolete by its mfr; I built with this device because I have
several still on hand. Any 1-deck, 1-pole, 6-position BBM switch with 30 degree position
intervals will do, and there is ample space on the board to fit a different switch
footprint with minimal rerouting of traces. Alpha produces other SR1712F rotary switches
like the 8-position `SR1712F-0108` which can also be dropped in directly. (As-is, the 7th
& 8th positions will cause the baseline voltage to float and the output will be undefined
when the switch is in either of these positions; you could cause the output to be defined
by simply connecting those two pins of the switch to ground.)
