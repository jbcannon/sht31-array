# Activation

Activating Particle Boron is simple and Particle has good documentation to aid with the activation. 

You will need
* Assembled datalogger from [previous step](logger-assembly.md)
* Bluetooth enabled Android or iOS device installed with Particle app downloaded from [Google Play](https://play.google.com/store/apps/details?id=io.particle.android.app&hl=en_US&gl=US) or [Apple Store](https://apps.apple.com/us/app/particle-iot/id991459054)
* One or more SHT31 sensor assemblies [from previous step](SHT-assembly.md)

With the battery from the assembled logger plugged in, follow the steps below to activate. [Steps to Activate Particle Boron](https://www.youtube.com/watch?v=xymSayKBGbg). Because your logger is powered by a battery, you do not need the USB connector. After following the steps in the video, you should have an activated device, and have updated firmware to the device which is automatically uploaded via the cellular connection.

Click image to watch video 

<a href="https://www.youtube.com/watch?v=xymSayKBGbg"><img src=https://img.youtube.com/vi/xymSayKBGbg/maxresdefault.jpg width=400></img></a>

# Testing

## Uploading Blink Sketch

* Once your Particle Boron is activated, it is best to complete a few tests to ensure your device is working properly.
* Log in to the [Particle Web IDE](https://build.particle.io/build)

<img src=../figs/setup-capture1.png width= 500></img>

- Under Example apps, select the Blink an LED sketch from the list (Red arrow)
- Check that the name of the device you just setup matches what is indicated by the yellow arrow. If not, click the name and indicate the correct device from the Particle Device list
- Once the correct device is selected, click the Flash button (blue arrow). This will upload the sketch to the Boron. 
- As the sketch is uploading, you should see a series of flashes. See here for a guide to [Particle Boron LED status indicators](https://docs.particle.io/tutorials/device-os/led/boron/)
  - Slow blinking green means the device is searching for signal.
  - Slow blinking cyan means Signal is found.
  - Fast blinking cyan means data transfer is occurring.
  - Magenta light appears when the app is flashed onto the device.
- Once the sketch is successfully updated, you should see a blue blink from the LED located next to the USB connector on the Boron.

<img src=../figs/setup-photo1.jpg width= 300></img>

## Testing SHT31 sensor

-	After successfully uploading the Blink sketch, connect a single SHT-31 sensor and upload a sketch that will upload the readings to Particles Cloud platform.
-	Release the 4 wires connected to the I<sup>2</sup>C multiplexer PCB assembly, and place each wire into a bread board as shown below. This will allow rapid connection of several single I<sup>2</sup>C devices to the Boron for testing and troubleshooting.
-	Connect one of the assembled SHT31 sensors to the corresponding cables. If you followed our construction, the pin associations are

| Wire | Pin |
| -- | -- |
| Red	| VCC |
| Black	| GND |
| Green	| SDA |
| White	| SCL |

<img src=../figs/setup-photo2.jpg width= 300></img>
<img src=../figs/setup-photo3.jpg width= 300></img><br>
<img src=../figs/setup-photo4.jpg width = 600></img>

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

- You will know the flash is successful when the cyan LED returns to blinking *breathe* mode. Click on the Console icon. You will see an Events table listing all status updates related to your Particle devices. The app you created reads and uploads the temperature and humidity once per second.
- Verify that humidity and temperature readings are valid. If you are not getting readings, check all wired connections with the sensor.
- In areas with a slow cellular connection, updates may occur at greater than 1 second intervals.
- Remove the SHT31-sensor form the breadboard and repeat seven times, connecting each additional sensor on the breadboard in turn until all sensors are tested.
 
# I<sup>2</sup>C and cloud upload
- The Particle console offers a convenient way to communicate directly with the datalogger, but does not serve for convenient data storage. To setup data logging from Particle Boron to Google Sheets, you will need to use the following steps.
- Follow the steps to [setup integration of Particle and Google Sheets](https://github.com/deancs/particlePostGoogle). This script guides you through the process to setup an empty GoogleSheet to contain data, integrate a script using the Script Editor, create and use a Particle security token, and link your script with a Particle Webhook
•	Create a new app in the Particle Web IDE and paste the following code and Flash the following script to your device. This code takes measurements at an `interval` of 5 seconds and uploads data continuously to the Cloud. Note that this requires a continuous cellular network connection that may deplete battery life in ~10 days. See below for code to decrease upload rates and extend battery life. 

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

* This code utilizes the `Particle.sleep()` function and local (RAM) data storage to increase battery life up to an estimated 180 days.
* The function takes a reading ever `INTERVAL` (in minutes) and stores data locally. Once the total number of records colelcted reaches `RECORDS_PER_UPLOAD` the data is uploaded to the Cloud.
* Note that < 80 kB of RAM data storage is available on Particle Boron, thus use caution if using `RECORDS_PER_UPLOAD` > 60 as RAM capacity may be exceeded.

```
#include <adafruit-sht31.h>
#include <TCA9534.h>

#define INTERVAL 15 // reading interval (in minutes), should be a divisor of 60 (e.g., 1, 2, 5, 6, 12, 15, 30)
#define RECORDS_PER_UPLOAD 12 // how many readings to take before uploading
char payload[RECORDS_PER_UPLOAD][1024] = {"","","","","","","","","","","",""};  // Put a set of apostrophes equal to the number of RECORDS_PER_UPLOAD.
#define TIMEZONE -4

// Instantiate Temperature - Humidity Sensor(s)
#define TCAADDR 0x70 // Address of TCA9548A I2C Multiplexer
#define PUBLICATION_DELAY 4000 // delay between Particle.publish() events (in ms) to prevent readings out of order.
Adafruit_SHT31 sht31 = Adafruit_SHT31();
FuelGauge fuel;
SystemSleepConfiguration config;
SYSTEM_MODE(SEMI_AUTOMATIC);

int record = 0;

void setup() {
    /// Connect to cloud and sync time.
    Particle.connect();
    waitUntil(Particle.connected);
    Particle.syncTime();
    waitUntil(Particle.syncTimeDone);
    delay(5s);
    Particle.disconnect(CloudDisconnectOptions().graceful(true).timeout(30s));
    Time.zone(TIMEZONE); 

    Wire.begin();
    RGB.control(true);
    for(int i=0; i<4; i++) { // flash color to indicate successful connection
        RGB.control(true);
        RGB.color(255,255,255);
        delay(200);
        RGB.color(10,0,0);
        delay(200);
        RGB.color(0,0,0);
    }
}

void loop() {
    if(Time.minute() % INTERVAL == 0 & Time.second() == 0){
        String current_time = Time.format(Time.now(), "%F %T");
        //String current_time = Time.timeStr();
        float t [8];
        float h [8];
        for (uint8_t bus=0; bus<8; bus++) {
          RGB.control(true);
          RGB.color(255,0,0);
          t[bus] = readTemp(bus, 0x44);
          h[bus] = readHumid(bus, 0x44);
          if(isnan(t[bus])) t[bus] = -100;
          if(isnan(h[bus])) h[bus] = -100;
          delay(200);
          RGB.color(0,0,0);
          delay(200);
        }
        float soc = fuel.getNormalizedSoC();
        float vbatt = fuel.getVCell();
        sprintf(payload[record],"{\"time\":\"%s\",\"record\":%d,\"charge\":%.1f,\"Vbatt\":%.2f,\"temp0\":%.1f,\"hum0\":%.1f,\"temp1\":%.1f,\"hum1\":%.1f,\"temp2\":%.1f,\"hum2\":%.1f,\"temp3\":%.1f,\"hum3\":%.1f,\"temp4\":%.1f,\"hum4\":%.1f,\"temp5\":%.1f,\"hum5\":%.1f,\"temp6\":%.1f,\"hum6\":%.1f,\"temp7\":%.1f,\"hum7\":%.1f}",
            current_time.c_str(), record, soc, vbatt, t[0], h[0], t[1], h[1], t[2], h[2], t[3], h[3], t[4], h[4], t[5], h[5], t[6], h[6], t[7], h[7]);
        Serial.print("Record "); Serial.println(record);
        Serial.println(payload[record]);
        Serial.println("=========");
        record = record + 1;        
        
        /// Once the appropriate number of records has been collected, upload them and dump data.
        if(record == RECORDS_PER_UPLOAD) {
            // reconnect to particle cloud
            Serial.println("Connecting to the cloud");
            if (!Particle.connected()) {
                    Particle.connect();
                    waitUntil(Particle.connected);
                    if(Particle.connected()) Serial.println("Succesfully connected"); else Serial.println("Connection unsucessful");
                    Particle.syncTime();
                    waitUntil(Particle.syncTimeDone);
            }
            
            Serial.println("Preparing to upload all records");
            // upload all records
            for(int i = 0; i < RECORDS_PER_UPLOAD; i++) {
                Serial.print("Uploading record: ");
                Serial.println(i);
                Serial.print(payload[i]);
                Serial.println("================");
                bool success = try_to_publish(payload[i], 3); //post to GoogleSheets
            }
            record = 0;
            Serial.println("Records uploaded to the cloud");
            Serial.println("Discconecting");
            Particle.disconnect(CloudDisconnectOptions().graceful(true).timeout(30s));
            Serial.println("Discconected");
        }
        
        Serial.println("Going to sleep");
        /// go to sleep after measurement
        config.mode(SystemSleepMode::STOP)
            .duration(INTERVAL * 1000 * 60 - 30000) // sleep for 30 seconds shorter than interval
            .flag(SystemSleepFlag::WAIT_CLOUD); // complete any cloud api activities before sleeping
        System.sleep(config);
        Serial.println("Waking up");
    }
}

// Function to read temperature from select TCA and address (bus = 0-7, addr = 0x44 or 0x45)
float readTemp(int bus, int addr) {
    Wire.beginTransmission(TCAADDR);
    Wire.write(1 << bus);
    Wire.endTransmission();
    if(!sht31.begin(addr)) return(-100); else {
        float temp = sht31.readTemperature();
        return(temp);    
        }
}

// Function to read humidity from select TCA and address (bus = 0-7, addr = 0x44 or 0x45)
float readHumid(int bus, int addr) {
    Wire.beginTransmission(TCAADDR);
    Wire.write(1 << bus);
    Wire.endTransmission();
    if(!sht31.begin(addr)) return(-100); else {
        float humid = sht31.readHumidity();
        return(humid);  
    }
}

bool try_to_publish(char payload[1024], int tries) {
    bool success = false;
    for(int i = 0; i < tries; i++) {
        if(success == false) {
            success = Particle.publish("postGoogle", payload);
            delay(PUBLICATION_DELAY);
        }
    }
    return(success);
}
```

# Deployment
- Reconnect the I<sup>2</sup>C multiplexer assembly to the Screw terminal block 
- Connect up to eight SHT31 sensors to the screw terminals on the SHT31 assembly. Depending on the enclosure you wish to use, you may need to feed the lines through a valve in the enclosure before screwing them down.
- Use a zip-tie to bundle the Particle Boron, Multiplexer Assembly, and battery into one unit, and place in the enclosure.
- Once turned on and connected, the device will upload 8 readings to the setup Google Sheets using the webhook and Google Script integration. Each device you use will create its own tab in the Google worksheet

<img src=../figs/loggerassembly-10.jpg height = 300></img> 
