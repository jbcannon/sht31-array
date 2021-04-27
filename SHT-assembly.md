# SHT31-D Temperature and Humidity array assembly protocol

Tanner Warren and Jeffery Cannon

<img src=docs/talltimbers_array_photo.jpg height=300></img>
<img src=docs/sht31-chip.jpg height=300></img>

## Tools
-	Soldering iron and lead-free solder
-	Brass Sponge to prolong soldering tip life
-	Wire strippers
-	Flush cutting pliers or other cutting tool
-	Bench-top clamp (not essential but greatly simplifies the process)
-	heat gun, blow dryer, or lighter for heat shrink

## Materials
-	SHT31-D breakout board (e.g., from [Aliexpress](https://www.aliexpress.com/item/32850554676.html) or [Amazon](https://www.amazon.com/Temperature-SHT31-D-Humidity-Breakout-Weather/dp/B073P6G2Q4/))
-	Shielded cable, 4 wire, solid core 22 AWG (lengths will vary)
-	Heat shrink tubing (1/4" and 1/2" diameter ([Amazon](https://www.amazon.com/gp/product/B01KYFZRQW))

## Assembly

-	Prep each end of the cable by stripping ~3 cm of the main shielding away from the four wires inside, and then ~1 cm of shielding away from each of the wires.

<img src=docs/shtassembly_1.png width=200></img>

-	Place the SHT31 sensor in the clamp or on a surface where the wires are easily fed through each pinhole on the board. Solder each wire individually in its respective place (suggested placements are indicated below). Good solder joints should resemble a bell-shape or Hershey’s kiss rather than a sphere-shape which indicates additional flux may be needed. See here for [tips on soldering breakout boards](http://www.youtube.com/watch?v=3230nCz3XQA&t=3m40s).

<img src=docs/shtassembly_2.png width=200></img>
<img src=docs/shtassembly_3.png width=200></img>
<img src=docs/shtassembly_4.png width=200></img>

Pin | Cable
-- | --
VIN | Red
GND | Black
SCL | White
SDA/SAA | Green

-	Trim the excess length from each wire to the top of the solder and straighten wire out so that the sensor and cable are in line. Test the sensor using an assembled tester and Arduino software to ensure all connections are correctly made.

<img src=docs/shtassembly_5.png width=200></img>
<img src=docs/shtassembly_6.png width=200></img>

-	Cut a piece of 1/4" diameter heat shrink long enough to cover the exposed wires of the sensor (no longer than 4 cm to ensure that the sensor can correctly slide into housing) and place on the cable. Use the heat gun/blow dryer to seal it in place. Then, cut a short piece (approximately 2 cm) of 1/2" diameter heat shrink and place over the soldered pins and most of the sensor. Do not cover the black square chip on the sensor with heat shrink. 
	
<img src=docs/shtassembly_7.png width=200></img>
<img src=docs/shtassembly_8.png width=200></img>
<img src=docs/shtassembly_9.png width=200></img>

-Feed the bare end of the cable through the channel in the sensor mount and place a piece of small diameter heat shrink on the cable before attaching a plug. 

<img src=docs/shtassembly_10.png width=200></img>



(Figure 10)
-Cut the wires of the plug down to ~2 cm long and strip ~0.5 cm away from the end (these wires are stranded and need to be twisted at the ends in order to keep internal wires together). 
-Tin the ends of each wire on both the plug and the cable. (Figure 11-13)
-Ensure the wires are lined up in the appropriate order as show in the “Plug Wiring” table. Then apply solder to the end of the soldering iron (held in the clamp if possible), take a wire in each hand, and simultaneously place them in the solder on the iron tip. Once they have enough solder on them, lift them out together and allow the solder to cool to complete the connection. This process can be repeated until a strong, even connection is made between the two. 
(Figure 14-16)   
- Cut small pieces of electrical tape and wrap them around each exposed connection between the cable and the plug (Figure 17). Trim any excess and then slide heat shrink down over the bare wires and use the heat gun/blow dryer to seal it. (Figure 18)
- Test the entire sensor using the assembled tester and Arduino software. (Figure 19)
- label the back of the sensor mount with the appropriate mounting height (depends on the length of the cable). Refer to the “Sensor Height” table.
