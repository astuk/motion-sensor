# motion-sensor
IOT Battery operated PIR Sensor

The NodeMCU Multisensor remixed from a sensor by Bruh Automation led me to create a simple motion sensor that can be run on an 18650 battery for months if not years. Using a Nodemcu v1.0 and making use of its deep sleep capability minimizes power usage only triggering a wifi connection and notifications after motion, then going back into a deep sleep.

Parts:
- Nodemcu Development board
- PIR Sensor
- 18650 Battery
- Some wires
- Blynk account
- 1k resistor
- 10k resistor
- 2N222 NPN Transistor

![nodemcu_motion_sensor](nodemcu_motion_sensor.png)

3D printed enclosure can be downloaded from thingiverse, https://www.thingiverse.com/thing:2784417

Example code
```
/**************************************************************
 * IoT Motion Detector with Blynk
 * Blynk library is licensed under MIT license
 * This example code is in public domain.
 * 
 * Developed by Marcelo Rovai - 30 November 2016
 **************************************************************/
#include <ESP8266WiFi.h>
#define BLYNK_PRINT Serial    // Comment this out to disable prints and save space
#include <BlynkSimpleEsp8266.h>
char auth[] = "urownblynkapikey";

/* WiFi credentials */
char ssid[] = "yourssid";
char pass[] = "yourpass";

/* HC-SR501 Motion Detector */

void setup()
{
  Serial.begin(115200);
  delay(10);
  Blynk.begin(auth, ssid, pass);
}

void loop()
  {
  Blynk.notify("Motion detected?"); 
  Blynk.run();
  digitalWrite(LED_BUILTIN, LOW);    // turn the LED off by making the voltage LOW
  ESP.deepSleep(0); // enter deep sleep
}
```
