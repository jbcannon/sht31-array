# Overview

We have developed a temperature-humidity array for use in applications in forest and fire ecology. The following instructions provide step-by-step instructions for assembling the arrays and dataloggers. We also include software development and installation, and provide files to fabricate 3d-printed radiation shields, enclosures, and files necessary for manufacturing printed circuit boards for multiplexing.

<figure>
<img src=figs/sensor-fig.PNG></img>
<figcaption align = "center"><font size = -1>Figure 1. (a-f) Development of environmental monitoring using open-source platforms. (a) Datalogging assembly based on Particle Boron microprocessor on a screw terminal mount powered by a 3.7V 5000 mAH LiPo battery. Custom printed circuit board (PCB, red) includes I<sup>2</sup>C multiplexer chip allowing up to eight identically addressed sensors. (b) Datalogging assembly installed in weather resistant enclosure. (c) Comparison of Adafruit SHT31-D temperature and humidity sensor (left) and iButton Hygrochron (DS1932, right). (d) Minimalist radiation shield mount with installed SHT31-D sensor. (e) Custom PCB to use I<sup>2</sup>C multiplexer with 4-pin screw terminals. (f) 5-fin radiation shield 3D printed with PETG.<font></figcaption>
</figure>

Each section begins with materials required for assembly. Please read all instructions before begining to ensure all necessary materials are available. The material presented below details the construction of sensor and data loggers used in Cannon et al. XXXX. See manuscript for complete details on theory and applications.

* Fabricate [temperature and humidity sensor arrays](#SHT31-D-Sensor-arrays) (8x sensors)
* Fabricate 3d printed radiation shields
* Prepare Particle Boron-based dataloggers
  * Testing Particle Boron
  * Programing Particle Boron
  * Setting up cellular cloud data upload
* Fabricate datalogger assembly
* Sensor array deployment 

# SHT31-D Sensor arrays



# 3D printing

We currently use two types of 3d printed radiation sheilds: a minimalist sheild, and a larger enclosed, multi-tiered sheild for longer-term abiotic monitoring. All sheilds are 3-printed in PETG use a PRUSA MK3S+ printer.

Data loggers require 

Include files and print settings for

Large radiation sheild
Minimal radiation sheild

Photos/assembly instructions?


readme: print settings
Prusa PETG ???
infill?

# Hardware

for each of these need: Schematic, BOM, .brd Gerbers, PDF of top/bottom layers

Datalogger (old) -- explanation of unreliability, link to Margay
TCA breakout board

#  Software

Code for TCA using Arduino UNO...
Code for data logger (old)
