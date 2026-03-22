# EXP-4-Home Automation System with IOT

# Aim:
To make a Lamp at home (230 V AC) On / Off using ESP8266, IFTT Google Assistance and Blynk IoT mobile application. 
# Hardware / Software Tools required :
* PC with Internet connection
* Micro USB cable
* Wifi connection for ESP8266 (Use any mobile hotspot or Router)
* ESP8266 Board
* Mobile Phone with Blynk App installed
* IFTT for Google Voice Assistance
* 9 W Bulb and Relay control
* Arduino software 
* Jumper Wires

# Circuit Diagram:
<img width="1295" height="727" alt="image" src="https://github.com/user-attachments/assets/a3e68af3-4caa-413d-9ffe-fb49a49c84b0" />



# Theory: 


Blynk is an IoT platform for iOS or Android smartphones that is used to control Arduino, Raspberry Pi and NodeMCU via the Internet. This application is used to create a graphical interface or human machine interface (HMI) by compiling and providing the appropriate address on the available widgets.In this experiment we use ESP8266 to control a 220-volt lamp from a web server. But you can also use the same procedure to control fans, lights, AC, or other electrical devices that you want to control remotely.
Relay is an electromechanical device that is used as a switch between high current and low current devices. When the coil in the relay gets fully energized, the contact shifts from the normally open position to the normally closed position. Light bulbs usually operate on 120V or 220V AC power supply. We cannot interface these AC loads directly with the ESP8266 development board, or it will damage the board. We have to use a relay between the ESP8266 and the lamp. 
Google Assistant and IFTTT work together to let you control services with voice commands. When you say a set phrase, Google Assistant processes it and sends it to IFTTT as a trigger. If the phrase matches an applet you've created, IFTTT performs the linked action—like turning on a light or sending a message. Everything runs in the cloud, making it easy to automate tasks with just your voice, as long as the command is correctly matched and all services are online.
When we apply an active high signal to the signal pin of the relay module from any microcontroller like ESP8266, the relay contact moves from the normally open to the normally closed position. It makes the circuit complete, and the output load turns on.


# Program:
~~~
#include <Servo.h>
#include <LiquidCrystal.h>

LiquidCrystal lcd(A1,10,9,6,5,3);
float value;
int tmp = A0;
const int pingPin = 7;
int servoPin = 8;

Servo servo1;

void setup() {
  Serial.begin(9600);
  servo1.attach(servoPin);
  lcd.begin(16, 2);

  pinMode(2, INPUT);    
  pinMode(4, OUTPUT);   
  pinMode(11, OUTPUT);  
  pinMode(12, OUTPUT);  
  pinMode(13, OUTPUT);  
  pinMode(A0, INPUT);   
}

void loop() {
  long duration, cm;
  pinMode(pingPin, OUTPUT);
  digitalWrite(pingPin, LOW);
  delayMicroseconds(2);
  digitalWrite(pingPin, HIGH);
  delayMicroseconds(5);
  digitalWrite(pingPin, LOW);

  pinMode(pingPin, INPUT);
  duration = pulseIn(pingPin, HIGH);
  cm = microsecondsToCentimeters(duration);

  if(cm < 40) {
    servo1.write(90);
    lcd.setCursor(0,1);
    lcd.print("Door:OPEN   ");
  } else {
    servo1.write(0);
    lcd.setCursor(0,1);
    lcd.print("Door:CLOSED ");
  }

  int pir = digitalRead(2);
  if(pir == HIGH) {
    digitalWrite(4, HIGH);
    lcd.setCursor(10,0);
    lcd.print("LED:ON ");
  } else {
    digitalWrite(4, LOW);
    lcd.setCursor(10,0);
    lcd.print("LED:OFF");
  }

  
  value = analogRead(tmp) * 0.004882814;
  value = (value - 0.5) * 100.0;
  lcd.setCursor(0,0);
  lcd.print("Tmp:");
  lcd.print(value);

  Serial.print("temperature: ");
  Serial.println(value);

  if(value > 20) {
    digitalWrite(12, HIGH);  // Hot LED ON
    digitalWrite(13, LOW);
  } else {
    digitalWrite(12, LOW);
    digitalWrite(13, HIGH);  // Cold LED ON
  }

  delay(500);
}

long microsecondsToCentimeters(long microseconds) {
  return microseconds / 29 / 2;
}
~~~


# Procedure:
*	Make the circuit connection as per the diagram. In the mobile, download and “Blynq IoT” application using Google play store and Install it. Create log in ID and Password.
*	Connect the IN pin of the Relay module to D1 pin of NodeMCU (ESP8266).
*	Connect VCC of the Relay of NodeMCU. Connect GND of the Relay to GND of NodeMCU. 
*	Connect your AC bulb to the Relay’s switch terminal securely.
*	Install ESP8266 board in Arduino IDE via Board Manager. Select board: NodeMCU 1.0 (ESP-12E Module).
*	Include necessary libraries: ESP8266WiFi and ESP8266WebServer.
*	In the code, configure Wi-Fi SSID and Password.
*	Set up a web server that responds to /on and /off URLs.
*	Upload the code to the ESP8266 using a micro USB cable.
*	Get Local IP Address After uploading, open Serial Monitor to find the local IP address of ESP8266.
*	Create Applets on IFTTT - For "This", select Google Assistant → "Say a simple phrase". Command: "Turn on the light". For "That", choose Webhooks → "Make a web request". 
*	Repeat to create another applet for command with URL.
*	Test the System - Google Assistant triggers IFTTT → sends Webhook to ESP8266 → turns ON the relay (light).
*	Say "Turn off the ligh to switch it OFF, Say "Turn on the light" to switch it ON.


# Output:


https://github.com/user-attachments/assets/53eb5884-270f-42f2-9109-77e90176da00



# Result:
Thus, Home Automation System with IOT was successfully implemented using TinkerCad.

