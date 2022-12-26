# Project 07: Flowing Water Light

1.  **Introduction：**

In our daily life, we can see many billboards composed of different
colors of LED. They constantly change the light (like water) to attract
customers' attention. In this project, we will use ESP32 to control 10
leds to achieve the effect of flowing water.

2.  **Components：**

|                                    |                        |                        |                        |
| ---------------------------------- | ---------------------- | ---------------------- | ---------------------- |
| ![](/media/e380dd26e4825be9a768973802a55fe6.png) |                        |                        |
| ESP32\*1                           | Breadboard\*1          |                        |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| Red LED\*1                         | 220Ω Resistor\*1       | Jumper Wires           | USB Cable\*1           |

3.  **Wiring diagram :**

![](/media/548f889607bdb0ce017c58f323c85dfa.png)

**Note:**

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

4.  **Project code：**

This project is designed to make a flowing water lamp. Which are these
actions: First turn LED \#1 ON, then turn it OFF. Then turn LED \#2 ON,
and then turn it OFF... and repeat the same to all 10 LEDs until the
last LED is turns OFF. This process is repeated to achieve the
“movements” of flowing water.

Codes used in this tutorial are saved in”**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
07：Flowing Water Light”, and double left-click
“Project\_07\_Flowing\_Water\_Light.py”.

![](/media/67c86d2d042de2cc00093ca0b608bec5.png)

    from machine import Pin
    import time
    
    #Use an array to define 10 GPIO ports connected to LED Bar Graph for easier operation.
    pins = [22, 21, 19, 18, 17, 16, 4, 0, 2, 15]
    #Use two for loops to turn on LEDs separately from left to right and then back from right to left
    def showLed():
        for pin in pins:
            print(pin)
            led = Pin(pin, Pin.OUT)
            led.value(1)
            time.sleep_ms(100)
            led.value(0)
            time.sleep_ms(100)        
        for pin in reversed(pins):
            print(pin)
            led = Pin(pin, Pin.OUT)
            led.value(1)
            time.sleep_ms(100)
            led.value(0)
            time.sleep_ms(100)
              
    while True:
        showLed()

**5. Project result：**

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/d6dc066d1004176c398b7c7b1588836a.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that 10 LEDs will light up from left to right
and then back from right to left. Press“Ctrl+C” or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” to exit the program.

![](/media/9ccd5984375ca74cf3949e0042db25c6.png)

![](/media/912e2c3f88b522b89b9935548bae3bd9.png)
