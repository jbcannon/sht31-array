# Overview

We have developed an open-platform temperature-humidity array for use in applications in forest and fire ecology. The following instructions provide step-by-step instructions for assembling the arrays and dataloggers. We also include software development and installation, and provide files to fabricate 3d-printed radiation shields, enclosures, and files necessary for manufacturing printed circuit boards for multiplexing.

 <p><p>Each section begins with materials required for assembly. Please read all instructions before begining to ensure all necessary materials are available. The material presented below details the construction of sensor and data loggers used in Cannon et al. XXXX. See manuscript for complete details on theory and applications.

* Complete assembly of [Particle Boron dataloggers](#data-logger-assembly-particle-boron-with-multiplexer) (1x)
* Fabricate [3d printed radiation shields](#3d-printed-radiation-shields) (8x shields)
* Fabricate [temperature and humidity sensor arrays](#SHT31-D-Sensor-arrays) (8x sensors)
* [Setting up Particle Boron-based dataloggers](#setup-and-test-boron-dataloggers)
  * Testing Particle Boron
  * Programing Particle Boron
  * Setting up cellular cloud data upload
 
<figure>
<img src=figs/sensor-fig.PNG></img>
<figcaption align = "center"><font size = -2>Figure 1. (a-f) Development of environmental monitoring using open-source platforms. (a) Datalogging assembly based on Particle Boron microprocessor on a screw terminal mount powered by a 3.7V 5000 mAH LiPo battery. Custom printed circuit board (PCB, red) includes I<sup>2</sup>C multiplexer chip allowing up to eight identically addressed sensors. (b) Datalogging assembly installed in weather resistant enclosure. (c) Comparison of Adafruit SHT31-D temperature and humidity sensor (left) and iButton Hygrochron (DS1932, right). (d) Minimalist radiation shield mount with installed SHT31-D sensor. (e) Custom PCB to use I<sup>2</sup>C multiplexer with 4-pin screw terminals. (f) 5-fin radiation shield 3D printed with PETG.<font></figcaption>
</figure>

 # Data logger Assembly (Particle Boron with multiplexer)
 
 Our system uses Particle Boron microcontrollers which have cellular network capabilities allowing remote data upload,  comprehensive documentation, and support a number of analog and digital devices using I<sup>2</sup>C or SPI. Our system uses multiple identically addressed SHT-31 sensors which requires a multiplexer to allow reading of multiple sensors, thus we have created a custom printed circuit board that needs to be ordered or made.
 
<img src=figs/loggerassembly-10.jpg width=200></img>
<img src=figs/tca-pcb-gerber.PNG height=200></img>
<img src=figs/loggerassembly-5.jpg width=200></img>

 Follow the link to find complete instructions to <a href=pages/logger-assembly.md>assemble Particle Boron datalogger and multiplexer</a>

 # SHT31-D Sensor arrays

The SHT-31D sensors is an accurate temperature and humidity sensor with an accuracy of ±0.3°C and ±2% relative humidty. The sensor uses I<sup>2</sup>C connections and is therefore compatabile with a wide variety of other I<sup>2</sup>C digital sensors allowing building more complex micro-metereological stations.

 Follow the link to find complete instructions to <a href=pages/SHT-assembly.md>building SHT-31 sensor arrays</a>
 
<img src=figs/sht31-chip.jpg width=200></img>
<img src=figs/shtassembly_5.png width=200></img>

# 3D Printed radiation shields

To house the SHT31-D sensors, we provide plans and printing instructions for two radiation shields, including a minimalist radiation shield and a mulit-fin radiation sheild. 

Follow the link to find 3D models, photos, and printer settings for <a href=pages/3dprint.md>printing the radiation sheilds</a> on a PRUSA MK3 printer, or similar

<img src=figs/shieldprint-3.jpg width=200></img>
<img src=figs/shieldprint-6.jpg width=200></img>
# Setup and test Boron dataloggers

Particle Boron offers a platform for interfacing with I<sup>2</sup>C sensors and connects to the web via cellular networks. 

Follow the link to find complete instructions to <a href=pages/boron-setup.md>activate and test Boron dataloggers<a/> with the SHT-31 sensors. The link includes instructions to activate through the Particle app for Android and iOS, testing upload apps and measurements, setting up cloud integration with Google Sheets, and deployment.

<img src=figs/setup-capture1.png width=200></img>
<img src=figs/setup-photo4.jpg height=200></img>
