# Project 30：Ultrasonic Ranger

1. Introduction：  
**The HC-SR04 ultrasonic sensor is a very affordable distance
sensor, mainly used for obstacle avoidance in various robotic
projects. It is also used for water level sensing and even as a
parking sensor. We treat the ultrasonic sensors as bat's eyes,, in
the dark, bats can still identify objects in front of them and
directions through ultrasound. In this project, we use ESP32 to
control a ultrasonic sensor and LEDs to simulate ultrasonic
rangefinder.

2. Components：

|                                    |                        |                        |                             |  |
| ---------------------------------- | ---------------------- | ---------------------- | --------------------------- |  |
| ![](/media/7eb361d680dfa351f07f8527aeb37abd.png) |  |
| ESP32\*1                           | Breadboard\*1          | Ultrasonic Sensor\*1   | Red LED\*4                  |  |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)      |  |
| M-F Dupont Wires                   | 220ΩResistor\*4        | Jumper Wires           | USB Cable\*1                |  |

3. Component knowledge：

**HC-SR04 Ultrasonic Sensor :** Like bats, sonar is used to determine
the distance to an object. It provides accurate non-contact range
detection, high-precision and stable readings. Its operation is not
affected by sunlight or black materials, just like a precision camera
(acoustically softer materials like cloth are difficult to detect). It
has an ultrasonic transmitter and receiver.

![](/media/e6f6037071e434febf7090b56ac35802.png)

In front of the ultrasonic sensor are two metal cylinders, these are the
converters. The converters convert the mechanical energy into an
electrical signal. In the ultrasonic sensor, there are transmitting
converters and receiving converters. The transmitting converter converts
the electric signal into an ultrasonic pulse, and the receiving
converter converts the reflected ultrasonic pulse back to an electric
signal. If you look at the back of the ultrasonic sensor, you will see
an IC behind the transmitting converter, which controls the transmitting
converter. There is also an IC behind the receiving converter, which is
a quad operational amplifier that amplifies the signal generated by the
receiving converter into a signal large enough to be transmitted to the
Microcontroller.

**Sequence diagrams:**

The figure shows the sequence diagram of the HC-SR04. To start the
measurement, the Trig of SR04 must receive at least 10us high pulse
(5V), which will activate the sensor to emit 8 cycles of 40kHz
ultrasonic pulses, and wait for the reflected ultrasonic pulses. When
the sensor detects ultrasound from the receiver, it sets the Echo pin to
high (5V) and delays it by one cycle (width), proportional to the
distance. To get the distance, measure the width of the Echo pin.

![](/media/4114885ac4b6214953e3224d8c1d52c4.png)

Time = Echo pulse width, its unit is“us” (microseconds)

Distance in centimeters = time / 58

Distance in inches = time / 148

4. Read the distance value of the ultrasonic sensor:

We will start with a simple ultrasonic ranging and print the
measured distance.

![](/media/db430baa07e2e4d9ac9efca1950b953a.jpeg)

The HC-SR04 ultrasonic sensor has four pins, they are Vcc, Trig,
Echo and GND. The Vcc pin provides the power source for generating
ultrasonic pulses and is connected to Vcc (+5V). The GND pin is
grounded. The Trig pin is where the Arduino sends a signal to start
the ultrasonic pulse. The Echo pin is where the ultrasonic sensor
sends information about the duration of the ultrasonic pulse to the
Control board. Wiring as shown below:

![](/media/a8d408be3629a2d288dbb30bd60007af.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
30：Ultrasonic Ranger”, and then double left-click“Project
30.1\_Ultrasonic\_Ranging.py”.

![](/media/9a98506ef88252af88f0ac0c2ed3bb65.png)

    from machine import Pin
    import time
    
    # Define the control pins of the ultrasonic ranging module. 
    Trig = Pin(13, Pin.OUT, 0)
    Echo = Pin(14, Pin.IN, 0)
    
    distance = 0 # Define the initial distance to be 0.
    soundVelocity = 340 #Set the speed of sound.
    
    # The getDistance() function is used to drive the ultrasonic module to measure distance,
    # the Trig pin keeps at high level for 10us to start the ultrasonic module.
    # Echo.value() is used to read the status of ultrasonic module’s Echo pin,
    # and then use timestamp function of the time module to calculate the duration of Echo
    # pin’s high level,calculate the measured distance based on time and return the value.
    def getDistance():
        Trig.value(1)
        time.sleep_us(10)
        Trig.value(0)
        while not Echo.value():
            pass
        pingStart = time.ticks_us()
        while Echo.value():
            pass
        pingStop = time.ticks_us()
        pingTime = time.ticks_diff(pingStop, pingStart) // 2
        distance = int(soundVelocity * pingTime // 10000)
        return distance
    
    # Delay for 2 seconds and wait for the ultrasonic module to stabilize,
    # Print data obtained from ultrasonic module every 500 milliseconds. 
    time.sleep(2)
    while True:
        time.sleep_ms(500)
        distance = getDistance()
        print("Distance: ", distance, "cm")

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/5a21a61d30170a248c677fc8e858116c.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you can use it to measure the distance between the
ultrasonic sensor and the object. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/90683074d2a7c854f72b290d8e37c4cc.png)

![](/media/ce873cf513307a15f9aa58078c8dd7d6.png)

5. Wiring diagram of the ultrasonic rangefinder：

Next, we will use ESP32 to control an ultrasonic sensor and 4 LEDs
to simulate ultrasonic rangefinder. Connect the line as shown below：

![](/media/910ed1be8be94411a090afb95af86d1a.png)

6. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
30：Ultrasonic Ranger”，and double left-click
“Project\_30.2\_Ultrasonic\_Ranger.py”.

![](/media/8d60daaed63147240ffbbf8f64c9e27a.png)

    from machine import Pin
    import time
    
    #Define the pins of four leds.
    led1 = Pin(4, Pin.OUT)
    led2 = Pin(0, Pin.OUT)
    led3 = Pin(2, Pin.OUT)
    led4 = Pin(15, Pin.OUT)
    
    # Define the control pins of the ultrasonic ranging module. 
    Trig = Pin(13, Pin.OUT, 0)
    Echo = Pin(14, Pin.IN, 0)
    
    distance = 0 # Define the initial distance to be 0.
    soundVelocity = 340 #Set the speed of sound.
    
    # The getDistance() function is used to drive the ultrasonic module to measure distance,
    # the Trig pin keeps at high level for 10us to start the ultrasonic module.
    # Echo.value() is used to read the status of ultrasonic module’s Echo pin,
    # and then use timestamp function of the time module to calculate the duration of Echo
    # pin’s high level,calculate the measured distance based on time and return the value.
    def getDistance():
        Trig.value(1)
        time.sleep_us(10)
        Trig.value(0)
        while not Echo.value():
            pass
        pingStart = time.ticks_us()
        while Echo.value():
            pass
        pingStop = time.ticks_us()
        pingTime = time.ticks_diff(pingStop, pingStart) // 2
        distance = int(soundVelocity * pingTime // 10000)
        return distance
    
    # Delay for 2 seconds and wait for the ultrasonic module to stabilize,
    # Print data obtained from ultrasonic module every 500 milliseconds. 
    time.sleep(2)
    while True:
        time.sleep_ms(500)
        distance = getDistance()
        print("Distance: ", distance, "cm")
        if distance <= 5:
           led1.value(1)
        else:
           led1.value(0)
        if distance <= 10:
           led2.value(1)
        else:
           led2.value(0)
        if distance <= 15:
           led3.value(1)
        else:
           led3.value(0)
        if distance <= 20:
           led4.value(1)
        else:
           led4.value(0)

7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/182a6e06c41cd57f73bae2f6950a02c0.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the "Shell" window of Thonny IDE will print
the distance between the ultrasonic sensor and the object, and the
corresponding LED will light up when we move our hand in front of the
ultrasonic sensor. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/f99aa3eac5106677d67897a5a67df5da.png)
