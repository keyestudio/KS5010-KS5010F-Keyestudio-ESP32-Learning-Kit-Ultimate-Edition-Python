# Project 16：Burglar Alarm

1. Introduction：

The human body infrared sensor measures the thermal infrared (IR) light
emitted by moving objects. The sensor can detect the movement of
people、animals and carsto trigger safety alarms and lighting. They are
used to detect movement and ideal for security such as burglar alarms
and security lighting systems. In this project, we will use the ESP32
control human body infrared sensor、buzzer and LED to simulate burglar
alarm.

2. Components：

|                                    |                               |                                                  |                             |                         |
| ---------------------------------- | ----------------------------- | ------------------------------------------------ | --------------------------- | ----------------------- |
| ![](/media/ef77f5a64c382157fc2dea21ec373fef.png) |                         |
| ESP32\*1                           | Human Body Infrared Sensor\*1 | Active Buzzer\*1                                 | Red LED\*1                  |                         |
| ![](/media/c4015c5c1b99b2eb674777c1e0dde82b.png) |
| Breadboard\*1                      | M-F Dupont Wires              | 220ΩResistor\*1                                  | USB Cable\*1                | Jumper Wires            |

3. Component knowledge：

![](/media/51dc6a366ebb066960c32263c37e0244.png)

**Human Body Infrared Sensor :** Its principle is that when some
crystals, such as lithium tantalate and triglyceride sulfate are heated,
the two ends of the crystal will generate an equal number of charges
with opposite signs. These charges can be converted into voltage output
by an amplifier. Due to the human body will release infrared light,
although relatively weak, can still be detected. When the Human Body
Infrared Sensor detects the movement of a nearby person,, the sensor
signal terminal outputs a high level 1, otherwise, it outputs low level
0. Special attention should be paid to the fact that this sensor can
detect people、animals and cars in motion, which cannot be detected in
static, and the maximum detection distance is about 7 meters.

**Note:** Since vulnerable to radio frequency radiation and temperature
changes, the PIR motion sensor should be kept away from heat sources
like radiators, heaters and air conditioners, as well as direct
irradiation of sunlight, headlights and incandescent light.

**Features:**

Maximum input voltage: DC 3.3 \~ 5V.

Maximum operating current: 50MA.

Maximum power: 0.3W.

Operating temperature: -20 \~ 85℃.

Output high level is 3V, low level is 0V.

Delay time: about 2.3 to 3 seconds.

Detection Angle: about 100 degrees.

Maximum detection distance: about 7 meters.

Indicator light output (when the output is high, it will light up).

Pin limiting current: 50MA.

**Schematic diagram:**

![](/media/9e1ec604aa6f9d4a3c1fe41d4bccd699.png)

4. Wiring Diagram：

![](/media/67fd78fc542f0e7c232d96a23fb90120.png)

5. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
16：Burglar Alarm”, and then double left-click
“Project\_16\_Burglar\_Alarm.py”.

![](/media/cf6f68bbb55f166717655ae1e966c033.png)

    # Import Pin and time modules.
    from machine import Pin
    import time
    
    # Define the pins of the Human infrared sensor,led and Active buzzer. 
    sensor_pir = Pin(15, Pin.IN)
    led = Pin(0, Pin.OUT)
    buzzer = Pin(2, Pin.OUT)
    
    while True: 
          if sensor_pir.value():
              buzzer.value(1)
              led.value(1)
              time.sleep(0.2)
              buzzer.value(0)
              led.value(0)
              time.sleep(0.2)         
          else:
              buzzer.value(0)
              led.value(0)

6. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/2b655761c46d32be3abfaf182c91a989.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that if the human body infrared sensor detects
someone moving nearby, the buzzer will continuously issue an alarm and
the LED will continuously flash. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/288014651f5494fe899c691e674ac6eb.png)
