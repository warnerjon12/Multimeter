# Multimeter
Board and software files for a basic multimeter

# Multimeter Circuit Ideas

Since I don't own an LCR meter, I wanted to find a way to measure my small capacitors with the parts I had on hand.
Using a fast microcontroller with a fast crystal oscillator, I can accurately measure period and duty cycle
for the output from a 555 timer. This can be used to measure RC values, from which I can measure capacitance
using known resistances. Using a reference capacitance, this can be setup to measure resistance or diode
drop the same way (although diode measurement also depends on the input voltage). This can be made to be
accurate using a C0G capacitor for reference to measure the resistances. This will account for
changes in temperature and whatnot.

## Voltage

Accurate voltage measurement of small positive voltages can be done using any of various ADCs,
including those built into many microcontrollers. Conventionally, inputs are brought into this range using
an auto-ranging divider circuit, but I took a different approach. Using an amplifier and diode-connected MOSFET,
a circuit can be made to approximate a scaled square root of an input voltage.
The circuit is made bidirectional by connecting two transistors in series. A feedback resistor linearizes
behavior for small voltages, and a feedback capacitor reduces ringing and improves the transient response.
A second amplifier offsets the voltage to put it in the needed range and provides buffering.
Theoretically, this scaling only loses one bit of precision, and allows a large range of input voltages.
The circuit can be calibrated using a reference input to account for temperature changes,
parasitics, etc.

# Microcontroller Choices

My recommendation is to use a Teensy 4.0 or 4.1, as it is Arduino compatible and has a fast processor and FPU.
For more accurate measurements, sub-microsecond timing can be implemented, although it is not normally
part of the Arduino library.
