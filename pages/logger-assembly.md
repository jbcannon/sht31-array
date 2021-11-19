# Particle Boron datalogger assembly

The Particle Boron is a development kit that supports cellular network. This guide illustrates tools, materials, and instruction for connecting the Particle Boron to a Multiplexer to allow up to 8 identically addressed I<sup>2</sup>C busses. 
 
 **Please note that if you only need one or two SHT-31 sensors attached to a data logger, the multiplexer is unnecessary. Simply attach the Boron to the Terminal block, and insert a battery**. The remaining steps involving the multiplexer are unnecessary and can be skipped.

## Tools
- Soldering iron and lead-free solder
- Wire strippers

## Materials

-	Particle Boron Kit (LTE CAT-M1) (NorAm) ([Particle](https://store.particle.io/collections/ethersim/products/boron-lte-cat-m1-noram-ethersim))
-	Adafruit Terminal Block Breakout FeatherWing ([Adafruit](https://www.adafruit.com/product/2926))
-	3.7V Lithium Battery with 2-pin female plug ([AliExpress](https://www.aliexpress.com/item/32846169676.html))
 
 If you would like to link the datalogger to more than two SHT-31 sensors, or have identically addressed I<sup>2</sup>, you will also need the following materials to allow multiplexing capabilities. 
 
- TCA9548A Multiplexer Module ([Adafruit](https://www.adafruit.com/product/2717) | [AliExpress](https://www.aliexpress.com/wholesale?SearchText=TCA9548A))
-	TCA9548A PCB Board ([contact me](mailto:jeffery.cannon@jonesctr.org) for a few, or see below for ordering a custom PCB)
-	5-6” length of 22AWG 4-wire solid core cable
-	9 4-pin screw terminals ([AliExpress](https://www.aliexpress.com/item/32919824190.html))

<img src=../figs/loggerassembly-1.jpg width=200></img>
<img src=../figs/loggerassembly-2.jpg width=200></img>
<img src=../figs/loggerassembly-3.jpg width=200></img>

## Assembly

 **Please note that if you only need one or two SHT-31 sensors attached to a data logger, the multiplexer is unnecessary. Simply attach the Boron to the Terminal block, and insert a battery** If you would like to add multiplexing capabilties, continue on.

- Order our custom, open source printed circuit board (PCB) which houses a multiplexer breakout board with screw terminal blocks. Download the \*.gerber files for our custom PCB. You can upload these files to any PCB printer. We use JLCPCB.com. Be sure to adjust surface finish to LeadFree HASL-RoHs. See this [video tutorial on ordering PCBs](https://www.youtube.com/watch?v=8r9syPCoZEs)

<img src=../figs/tca-pcb-gerber.PNG width=300></img>

Donwload and print custom PCB using the [Custom PCB \*.gerber](../files/Custom_PCB_gerber.zip) files.

- Insert the male header pins for TCA9548A into the custom PCB board. Solder all male header pins to the TCA9548A Multiplexer.

<img src=../figs/loggerassembly-4.jpg width=200></img>

- Insert a 4-pin screw terminal into each designated slot in the PCB board, and then solder each one. Make sure to apply a little extra solder to these in order to reinforce them for repeated use.

<img src=../figs/loggerassembly-5.jpg height=200></img>
<img src=../figs/loggerassembly-6.jpg height=200></img>

- Attach the antenna to the Particle Boron, and then dock the Particle Boron in the associated female header pins located on the Breakout board.
 
 <img src=../figs/loggerassembly-7.jpg width=200></img>
 
 - Strip the shielded cable on each end (~3-4cm on one end and 1-2cm on the other) and place the wires on the longer end in their respective places on the screw terminals of the Breakout board, which are: Red = 3v3; Black = GND; White = SCL; Green = SDA. Attach the assembled TCA9548A module to the Particle module with the short end of the cable, with wiring as: Red = VIN; Black = GND; Green = SDA; White = SCL.

<img src=../figs/loggerassembly-8.jpg width=200></img>
<img src=../figs/loggerassembly-9.jpg width=200></img>

- Plug the 3.7V battery into the Particle Boron using the 2-pin female plug, and arrange the completed components as shown for the most compact configuration (can be zip-tied to ensure they stay together but you may want to wait until all sensors are attached to allow access to ports).

<img src=../figs/loggerassembly-10.jpg width=200></img>
