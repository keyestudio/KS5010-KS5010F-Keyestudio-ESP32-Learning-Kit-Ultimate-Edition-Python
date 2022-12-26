# Project 27：Temperature Measurement

1. Introduction：**

LM35 is a common used and easy-to-use temperature sensor. It doesn't
require any other hardware and you only need an analog port. The
difficulty lies in compiling the code and converting the analog values
to Celsius temperature. In this project, we used a temperature sensor
and 3 LEDs to make a temperature tester. When the temperature sensor
touches different temperature objects, the LEDs will show different
colors.

2. Components：

|                                    |                             |                         |                             |                              |                         |
| ---------------------------------- | --------------------------- | ----------------------- | --------------------------- | ---------------------------- | ----------------------- |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)      |                              |                         |
| ESP32\*1                           | Breadboard\*1               | LM35\*1                 | USB Cable\*1                |                              |                         |
| ![](/media/e9a8d050105397bb183512fb4ffdd2f6.png) |
| 220Ω Resistor\*3                   | Red LED\*1                  | Yellow LED\*1           | Green LED\*1                | M-F Dupont Wires             | Jumper Wires            |

3. Component knowledge：

![](/media/0fded1cfe95575d0fa4aa03839d8e30d.png)

**Working principle of LM35 temperature sensor:** LM35 temperature
sensor is a widely used temperature sensor with a variety of package
types. At room temperature, it can achieve the accuracy of 1/4°C without
additional calibration processing. LM35 temperature sensor can produce
different voltage according to different temperatures, when the
temperature is 0 ℃, it output 0V; If increasing 1 ℃, the output voltage
will increase 10mv. The output temperature is 0℃ to 100℃, the conversion
formula is as follows：

![](/media/0dfa07fa69f2a98658a3822c2da93bf7.jpeg)

4. Read the temperature value of the LM35：

We first use a simple code to read the value of the temperature sensor
and printing them out, wiring diagram is shown below：

![](/media/041471b9fabd75ef9dc3951598e342f8.png)

LM35 output is given to analog pin GPIO36 of the ESP32, this analog
voltage is converted to its digital form and processed to get the
temperature reading.

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open “Thonny”，click “This computer”→“D:”→“2. Python Projects”→“Project
27：Temperature Measurement”, and then double left-click
“Project\_27.1\_Read\_LM35\_Temperature\_Value.py”.

![](/media/f56863aa679f50e359d7342aa70e78b7.png)

    from machine import ADC, Pin
    import time
    
    # Turn on and configure the ADC with the range of 0-3.3V 
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_12BIT)
    conversion_factor = 3.3 / (4095)
    
    while True:
        adcVal=adc.read()
        reading = adcVal * conversion_factor 
        temperature = reading * 102.4 
        print(temperature)
        time.sleep(1)

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/19d52dd11d8c7b913b927e1fb6f0cf79.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the "Shell" window of Thonny IDE will print
the temperature values read by the LM35 temperature sensor. Hold the
LM35 element by hand, the temperature value read by the LM35 temperature
sensor will change. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/69e84efe8c0a9e61ec6a3382e9970c6d.png)

![](/media/551c6dbd30abab7a45c501b31a0502c5.png)

5.  diagram of the temperature measurement：

Now we use a LM35 temperature sensor and three LED lights to do a
temperature test. When the LM35 temperature sensor senses different
temperatures, different LED lights will light up. Follow the diagram
below for wiring.

![](/media/831ebf50a9b59c744cbd93ac2170d64b.png)

6. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
27：Temperature Measurement”，and then double left-click
“Project\_27.2\_Temperature\_Measurement.py”.

(Note: The temperature threshold in the code can be reset itself as
required.)![](/media/a215dcfe0e2815ad9466c80da372ea8a.png)

    from machine import ADC, Pin
    import time
    
    # Turn on and configure the ADC with the range of 0-3.3V 
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_12BIT)
    conversion_factor = 3.3 / (4095)
    
    # create red led object from Pin 15, Set Pin 15 to output
    led_red = Pin(15, Pin.OUT)  
    # create yellow led object from Pin 2, Set Pin 2 to output
    led_yellow = Pin(2, Pin.OUT)
    # create green led object from Pin 4, Set Pin 4 to output
    led_green = Pin(4, Pin.OUT) 
    
    while True:
        adcVal=adc.read()
        reading = adcVal * conversion_factor 
        temperature = reading * 102.4 
        print(temperature)
        time.sleep(0.2)
        if temperature <20:
            led_red.value(1)  # Set red led turn on
            led_yellow.value(0) # Set yellow led turn off 
            led_green.value(0)  # Set green led turn off
        elif temperature >=20 and temperature <25:
            led_red.value(0)  # Set red led turn off
            led_yellow.value(1) # Set yellow led turn on 
            led_green.value(0)  # Set green led turn off
        else:
            led_red.value(0)  # Set red led turn off
            led_yellow.value(0) # Set yellow led turn off 
            led_green.value(1)  # Set green led turn on

7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/37b5d4501e55e96851c5d0627feef1ed.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the "Shell" window of Thonny IDE will print
the temperature values read by the LM35 temperature sensor. When the
LM35 temperature sensor senses different temperatures, different LEDS
will light up. Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”to exit the program.

![](/media/cc771fb29f595a6c9049e2e442774a0b.png)
