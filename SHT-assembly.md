# SHT31-D temperature and Humidity array assembly protocol

Tanner Warren and Jeffery Cannon

<img src=figs/talltimbers_array_photo.JPG height=300></img>
<img src=figs/sht31-chip.jpg height=300></img>

## Tools
-	Soldering iron and lead-free solder
-	Brass Sponge to prolong soldering tip life
-	Wire strippers
-	Flush cutting pliers or other cutting tool
-	Bench-top clamp (not essential but greatly simplifies the process)
-	heat gun, blow dryer, or lighter for heat shrink

## Materials
-	SHT31-D breakout board (e.g., from [Adafruit](https://www.adafruit.com/product/2857), [Aliexpress](https://www.aliexpress.com/item/32850554676.html) or [Amazon](https://www.amazon.com/Temperature-SHT31-D-Humidity-Breakout-Weather/dp/B073P6G2Q4/))
-	Shielded cable, 4 wire, solid core 22 AWG (lengths will vary)
-	Heat shrink tubing (1/4" and 1/2" diameter ([Amazon](https://www.amazon.com/gp/product/B01KYFZRQW)))
-	JST or other 4-pine connectors (if your datalogger requries it). The Particle Boron-based dataloggers we recommend do not require connectors.

## Assembly

- Cut a piece of 22 AWG 4-wire cable to the desired length. For our 8 sensor array, we mounted a data logger at 1.5 m. For this height, cut lenghts according to the following table

Height | Cable length
-- | --
6 m | ~5 m
5 m | ~4 m
4 m | ~3 m
3 m | ~2 m
2 m | ~0.75-1 m
1 m | ~0.75-1 m
0.5 m | ~1.5 m
0 m | ~2 m

- Prep each end of the cable by stripping ~3 cm of the main shielding away from the four wires inside, and then ~1 cm of shielding away from each of the wires.

<img src=figs/shtassembly_1.png width=200></img>

- Place the SHT31 sensor in the clamp or on a surface where the wires are easily fed through each pinhole on the board. Solder each wire individually in its respective place (suggested placements are indicated below). Good solder joints should resemble a bell-shape or Hershey’s kiss rather than a sphere-shape which indicates additional flux may be needed. See here for [tips on soldering breakout boards](http://www.youtube.com/watch?v=3230nCz3XQA&t=3m40s).

<img src=figs/shtassembly_2.png width=200></img>
<img src=figs/shtassembly_3.png width=200></img>
<img src=figs/shtassembly_4.png width=200></img>

Pin | Cable
-- | --
VIN | Red
GND | Black
SCL | White
SDA/SAA | Green

-	Trim the excess length from each wire to the top of the solder and straighten wire out so that the sensor and cable are in line. Test the sensor using an assembled tester and Arduino software to ensure all connections are correctly made.

<img src=figs/shtassembly_5.png width=200></img>
<img src=figs/shtassembly_6.png width=200></img>

-	Cut a piece of 1/4" diameter heat shrink long enough to cover the exposed wires of the sensor (no longer than 4 cm to ensure that the sensor can correctly slide into housing) and place on the cable. Use the heat gun/blow dryer to seal it in place. Then, cut a short piece (approximately 2 cm) of 1/2" diameter heat shrink and place over the soldered pins and most of the sensor. Do not cover the black square chip on the sensor with heat shrink. 
	
<img src=figs/shtassembly_7.png width=200></img>
<img src=figs/shtassembly_8.png width=200></img>
<img src=figs/shtassembly_9.png width=200></img>

** NEED TO ADD LINK to MOUNT **

-Feed the bare end of the cable through the channel into the [3d printed sensor mount](#).

<img src=figs/shtassembly_10.png width=200></img>

- Repeat the above steps until you have 8 sesnor assemblies.
- **If your data logger uses screw terminals** (e.g., the Particle Boron-based datalogger which we recommend) then assembly of the a single unit is complete. 
- If if you would like to add a JST 4-pin plug or another connector for some devices, continue on to the additional steps. However, in our experience the JST plugs are brittle and thus somewhat finicky

<hr>

- **If you would like to connect a JST or another plug**, Slide a 3" piece of 1/4" diameter heat shrink on the cable before attaching a plug. Once the plug is installed you will no longer be able to add the heat shrink.
- Cut the wires of the plug down to ~2 cm long and strip ~0.5 cm away from the end (these wires are stranded and need to be twisted at the ends in order to keep internal wires together). Tin the ends of each wire on both the plug and the cable. (Figure 11-13)

<img src=figs/shtassembly_11.png width=200></img>
<img src=figs/shtassembly_12.png width=200></img>

-Ensure the wires are lined up in the appropriate order as show in the wiring table below. Then apply solder to the end of the soldering iron (held in the clamp if possible), take a wire in each hand, and simultaneously place them in the solder on the iron tip. Once they have enough solder on them, lift them out together and allow the solder to cool to complete the connection. This process can be repeated until a strong, even connection is made between the two. 

Plug | Cable | Sensor
-- | -- | --
Black | Red | VIN
Red | Black | GND
White | White | SCL
Yellow | Green |SDA/SAA

<img src=figs/shtassembly_13.png width=200></img>
<img src=figs/shtassembly_14.png width=200></img>
<img src=figs/shtassembly_15.png width=200></img>

- Cut small pieces of electrical tape and wrap them around each exposed connection between the cable and the plug. Trim any excess and then slide heat shrink down over the bare wires and use the heat gun/blow dryer to seal it.

<img src=figs/shtassembly_16.png width=200></img>
<img src=figs/shtassembly_17.png width=200></img>

- Label the back of the sensor mount with the appropriate mounting height (depends on the length of the cable). Refer to the “Sensor Height” table.
