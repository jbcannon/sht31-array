# Activation

Activating Particle Boron is simple and Particle has good documentation to aid with the activation. 

You will need
* Assembled datalogger  from previous step
* Bluetooth enabled Android or iOS device installed with Particle app downloaded from Google Play or Apple Store

With the battery from the assembled logger plugged in, follow the steps below to activate. [Steps to Activate Particle Boron](https://www.youtube.com/watch?v=xymSayKBGbg). Because your logger is powered by a battery, you do not need the USB connector. After following the steps in the video, you should have an activated device, and have updated firmware to the device which is automatically uploaded via the cellular connection.

Click image to watch video 

<a href="https://www.youtube.com/watch?v=xymSayKBGbg"><img src=https://img.youtube.com/vi/xymSayKBGbg/maxresdefault.jpg width=400></img></a>

# Testing

## Uploading Blink Sketch

* Once your Particle Boron is activated, it is best to complete a few tests to ensure your device is working properly.
* Log in to the Particle Web IDE

<img src=../figs/setup-capture1.png width= 500></img>

* Under Example apps, select the Blink an LED sketch from the list (Red arrow)
* Check that the name of the device you just setup matches what is indicated by the yellow arrow. If not, click the name and indicate the correct device from the Particle Device list
* Once the correct device is selected, click the Flash button (blue arrow). This will upload the sketch to the Boron. 
* As the sketch is uploading, you should see a series of flashes. Slow blinking green means the device is searching for signal. Slow blinking cyan means Signal is found. Fast blinking cyan means data transfer is occurring. You may see a brief magenta light as the sketch is flashed onto the device. See here for a guide to Particle Boron LED status indicators
* Once the sketch is successfully updated, you should see a blue blink from the LED located next to the USB connector on the Boron.

<img src=../figs/setup-photo1.jpg width= 300></img>

## Testing SHT31 sensor

-	After successfully uploading the Blink sketch, we will connect a single SHT-31 sensor and upload a sketch that will upload the readings to Particles Cloud platform.
-	Release the 4 wires connected to the I<sup>2</sup>C multiplexer PCB assembly, and place each wire into a bread board as shown below This will allow rapid connection of several single I<sup>2</sup>C devices to the Boron for testing and troubleshooting.
-	Connect one of the assembled SHT31 sensors to the corresponding cables. If you followed our construction, the pin associations are

| Wire | Pin |
| -- | -- |
| Red	| VCC |
| Black	| GND |
| Green	| SDA |
| White	| SCL |

<img src=../figs/setup-photo2.jpg width= 300></img>
<img src=../figs/setup-photo3.jpg width= 300></img>
<img src=../figs/setup-photo4.jpg width= 300></img>

-	In the Particle Web IDE, select the Code Symbol (< >) on the left hand side, and select Create New App
-	Name the app `sht31-single` or similar
-	Select the Libraries button from the lefthand side (bookmark) and search `adafruit-sht31`. Select the library, and click the “Include in Project” button. Select the app you just named and confirm its inclusion.
-	The following code reads the temperature and humidity of the logger and publishes it to Particles Console for viewing. Paste the following code into the code window and select the Flash button to upload the app.

```
// This app reads a single an SHT-31 sensor connected via I2C and uploads to Particle Console
#include <adafruit-sht31.h>
Adafruit_SHT31 sht31 = Adafruit_SHT31();

void setup() {
    Wire.begin();
    sht31.begin(0x44);
    delay(1000);
}

void loop() {
    if(Time.second() == 0){
      float t = sht31.readTemperature();
      float h = sht31.readHumidity();
      Particle.publish("temperature", String(t));
      Particle.publish("humidity", String(h));
      char payload[128] = "";
      sprintf(payload,"{\"temp\":%.2f,\"hum\":%.2f}", t, h);
      delay(1000);
    }
}
```

•	You will know the flash is successful when the cyan LED returns to blinking “breath” mode. Click on the Console icon. You will see an Events table listing all status updates related to your Particle devices. The app you created reads and uploads the temperature and humidity once per second.
•	Verify that humidity and temperature readings are valid. If you are not getting readings, check all wired connections with the sensor.
•	In areas with a slow cellular connection, readings may occur at great than 1 second intervals.
•	Remove the SHT31-sensor form the breadboard and place each additional sensor in turn until all sensors are tested.
 

I2C and cloud upload
•	The Particle console offers a convenient way to communicate directly with the datalogger, but does not serve for convenient data storage. To setup data logging from Particle Boron to Google Sheets, you will need to use the following steps.
•	Follow the steps to setup integration of Particle and Google Sheets https://github.com/deancs/particlePostGoogle . This script has you setup an empty GoogleSheet to contain data, integrate a script using the Script Editor, create and use a Particle security token, and link your script with a Particle Webhook
•	Create a new app in the Particle Web IDE and paste the following code and Flash the script to your device.

```
#include <adafruit-sht31.h>
#include <TCA9534.h>

const int interval = 5; // reading interval (in seconds), should be a divisor of 60 (e.g., 1, 2, 5, 6, 12, 15, 30)

// Instantiate Temperature - Humidity Sensor(s)
#define TCAADDR 0x70 // Address of TCA9548A I2C Multiplexer
Adafruit_SHT31 sht31 = Adafruit_SHT31();
FuelGauge fuel;

char payload[128] = "";

void setup() {
    Wire.begin();
}

void loop() {
    if(Time.second() % interval == 0){
        float t [8];
        float h [8];
        for (uint8_t bus=0; bus<8; bus++) {
          t[bus] = readTemp(bus, 0x44);
          h[bus] = readHumid(bus, 0x44);
          if(isnan(t[bus])) t[bus] = -100;
          if(isnan(h[bus])) h[bus] = -100;
        }
        float soc = fuel.getNormalizedSoC();
        float vbatt = fuel.getVCell();
        sprintf(payload,"{\"charge\":%.1f,\"Vbatt\":%.2f,\"temp0\":%.1f,\"hum0\":%.1f,\"temp1\":%.1f,\"hum1\":%.1f,\"temp2\":%.1f,\"hum2\":%.1f,\"temp3\":%.1f,\"hum3\":%.1f,\"temp4\":%.1f,\"hum4\":%.1f,\"temp5\":%.1f,\"hum5\":%.1f,\"temp6\":%.1f,\"hum6\":%.1f,\"temp7\":%.1f,\"hum7\":%.1f}", soc, vbatt, t[0], h[0], t[1], h[1], t[2], h[2], t[3], h[3], t[4], h[4], t[5], h[5], t[6], h[6], t[7], h[7]);
        Particle.publish("postGoogle", payload); //post to GoogleSheets
        delay(1s);
    }
}

// Function to read temperature from select TCA and address (bus = 0-7, addr = 0x44 or 0x45)
float readTemp(int bus, int addr) {
    Wire.beginTransmission(TCAADDR);
    Wire.write(1 << bus);
    Wire.endTransmission();
    sht31.begin(addr);
    delay(500);
    float temp = sht31.readTemperature();
    return(temp);    
}

// Function to read humidity from select TCA and address (bus = 0-7, addr = 0x44 or 0x45)
float readHumid(int bus, int addr) {
    Wire.beginTransmission(TCAADDR);
    Wire.write(1 << bus);
    Wire.endTransmission();
    sht31.begin(addr);
    float humid = sht31.readHumidity();
    return(humid);    
}
```

Deployment
•	Reconnect the i2C multiplexer assembly to the Screw terminal block 
•	Connect up to eight SHT1 sensors to the screw terminals on the SHT31 assembly. Depending on the enclosure you wish to use, you may need to feed the lines through a valve in the enclosure before screwing them down.
•	Use a zip-tie to bundle the Particle Boron, Multiplexer Assembly, and battery into one unit, and place in the enclosure.
[Photo of completed device]
•	Once turned on and connected, the device will upload 8 readings to the setup Google Sheets using the webhook and Google Script integration.
 
