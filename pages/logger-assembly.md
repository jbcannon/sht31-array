# Particle Boron datalogger assembly

Needs introduction and summary

## Tools
- Soldering iron and lead-free solder
- Wire strippers

## Materials

-	Particle Boron (LTE CAT-M1?)
-	Assembled Terminal Block Breakout FeatherWing
-	TAOGLAS FXUB63 Ultra Wide Band Antenna
-	5-6” length of 22AWG 4C Solid shielded cable
-	TCA9548A PCB Board
-	TCA9548A Multiplexer Module
-	9 4-pin screw terminals
-	3.7V Lithium Battery with 2-pin female plug 

<img src=../figs/loggerassembly-1.jpg width=200></img>
<img src=../figs/loggerassembly-2.jpg width=200></img>
<img src=../figs/loggerassembly-3.jpg width=200></img>

## Assembly

- Insert the male header pins for TCA9548A into the PCB board. Solder all male header pins to the TCA9548A Multiplexer.

<img src=../figs/loggerassembly-4.jpg width=200></img>

- Insert a 4-pin screw terminal into each designated slot in the PCB board, and then solder each one. Make sure to apply a little extra solder to these in order to reinforce them for repeated use.

<img src=../figs/loggerassembly-5.jpg height=200></img>
<img src=../figs/loggerassembly-6.jpg height=200></img>

- Attach the antenna to the Particle Boron, and then dock the Particle Boron in the associated female header pins located on the Breakout board.
 
 <img src=../figs/loggerassembly-7.jpg width=200></img>
 
 - Strip the shielded cable on each end (~3-4cm on one end and 1-2cm on the other) and place the wires on the longer end in their respective places on the screw terminals of the Breakout board, which are: Red = 3v3; Black = GND; White = SCL; Green = SDA. Attach the assembled TCA9548A module to the Particle module with the short end of the cable, with wiring as: Red = VIN; Black = GND; Green = SDA; White = SCL.

<img src=../figs/loggerassembly-8.jpg width=200></img>
<img src=../figs/loggerassembly-9.jpg width=200></img>

- Plug the 3.7V battery into the Particle Boron using the 2-pin female plug, and arrange the completed components as shown for the most compact configuration (can be zip-tied to ensure they stay together).

<img src=../figs/loggerassembly-10.jpg width=200></img>
