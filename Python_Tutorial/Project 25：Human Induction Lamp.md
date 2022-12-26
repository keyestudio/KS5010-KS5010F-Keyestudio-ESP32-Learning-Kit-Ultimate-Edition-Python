# Project 25：Human Induction Lamp

1. Introduction：

Human body induction lamp is used commonly in the dark corridor area.
With the development of science and technology, the use of the human
body induction lamp is very common in our real life, such as the
corridor of the community, the bedroom of the room, the garage of the
dungeon, the bathroom and so on. The human induction lamp are generally
composed of a human body infrared sensor, a led, a photoresistor sensor
and so on.

In this project, we will learn how to use a Human Body Infrared Sensor,
a led, and a photoresistor to make a human induction lamp.

2. Components：

|                                    |                               |                             |                             |                         |                         |
| ---------------------------------- | ----------------------------- | --------------------------- | --------------------------- | ----------------------- | ----------------------- |
| ![](/media/8cf9b1b3a5fec374cde3c5f0537567cb.png)  |                         |                         |
| ESP32\*1                           | Breadboard\*1                 | Red LED\*1                  | 10KΩResistor\*1             |                         |                         |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| Photoresistor\*1                   | Human Body Infrared Sensor\*1 | 220ΩResistor\*1             | M-F Dupont Wires            | Jumper Wires            | USB Cable\*1            |

3. Wiring Diagram：

![](/media/69f49d65054a9246acf4adc534217027.png)

4. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
25：Human Induction Lamp”，and then double left-click
“Project\_25\_Human\_ Induction\_Lamp.py”.

![](/media/6f5857ddbf0ed961db221b132bce29c4.png)

    from machine import Pin, ADC
    import time
     
    # Human infrared sensor pin
    human = Pin(15, Pin.IN)
     
    # Initialize the photosensitive sensor pin to GP36 (ADC function)
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_10BIT)
    #create the LED object from Pin 4, Set Pin 4 to output 
    led = Pin(4, Pin.OUT)
    
    def detect_someone():
        if human.value() == 1:
            return True
        return False
     
    abc = 0
     
    while True:
        adcVal=adc.read()
        if adcVal >= 500:
            if detect_someone() == True:
                abc += 1
                led.value(1)
                print("value=", abc)
                time.sleep(1)
            else:
                if abc != 0:
                    abc = 0
                    led.value(0)
        else:
            led.value(0)
     
        time.sleep(0.1)

5. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/bbdaf50534db57036e34af09f5dc7b09.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that When your hand covers the photosensitive
part of the photoresistor to simulate darkness, then shake your other
hand in front of the Human Body Infrared Sensor, the external LED will
light up, and after a delay of a few seconds, the external LED will
automatically turn off.  

At the same time, the "Shell" window of Thonny IDE will print the delay
time when the external LED lights up. If the photosensitive part of the
photoresistor is not covered, then shake your hand  in front of  the
human infrared sensor and the LED is turned off. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/d6fe49c1a8e901b8e7dcc4deaee954d7.png)

![](/media/af94ad9d2f008956592ee64e207aa8b5.png)
