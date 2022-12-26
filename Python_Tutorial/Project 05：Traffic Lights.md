# Project 05：Traffic Lights

1.  **Introduction：**

Traffic lights are closely related to people's daily life, which
generally show red, yellow, and green. Everyone should obey the traffic
rules, which can avoid many traffic accidents. In this project, we will
use ESP32 and some LEDs (red, green and yellow) to simulate the traffic
lights.

2.  **Components：**

|                                    |                        |                             |                         |  |
| ---------------------------------- | ---------------------- | --------------------------- | ----------------------- |  |
| ![](/media/0c1b0f91b4e56bcbc235d06b48809ac9.png) |  |
| ESP32\*1                           | Bread board\*1         | Red LED\*1                  | Yellow LED\*1           |  |
| ![](/media/c801a7baee258ff7f5f28ac6e9a7097b.png)  |  |
| GreenLED\*1                        | USB Cable\*1           | 220Ω Resistor\*3            | Jumper Wires            |  |

**3.** **Wiring diagram：**

![](/media/a991f5cc6f8759eca3b9d01f95fe4854.png)

**Note:**

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

**4. Project code：**

Codes used in this tutorial are saved in”**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
05：Traffic Lights”. and double left-click
“Project\_05\_Traffic\_Lights.py”.

![](/media/3e7a7b6c0b24bb17c40d2df0a774a6af.png)

    from machine import Pin
    import time
    
    led_red = Pin(0, Pin.OUT)  # create red led object from Pin 0, Set Pin 0 to output
    led_yellow = Pin(2, Pin.OUT)  # create yellow led object from Pin 2, Set Pin 2 to output
    led_green = Pin(15, Pin.OUT) # create green led object from Pin 15, Set Pin 15 to output
    
    while True:
        led_red.value(1)  # Set red led turn on
        time.sleep(5)   # Sleep 5s
        led_red.value(0) # Set red led turn off 
        led_yellow.value(1)
        time.sleep(0.5)
        led_yellow.value(0)
        time.sleep(0.5)
        led_yellow.value(1)
        time.sleep(0.5)
        led_yellow.value(0)
        time.sleep(0.5)
        led_yellow.value(1)
        time.sleep(0.5)
        led_yellow.value(0)
        time.sleep(0.5)
        led_green.value(1)
        time.sleep(5) 
        led_green.value(0) 

5.  **Project result：**

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/2065c1fd3ae9e84526ccf18f1f5f0cc8.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see are below:

① First, the green light will be on for five seconds and then off; 

② Next, the yellow light blinks three times and then goes off;

③ Then, the red light goes on for five seconds and then goes off;

④ Repeat steps 1 to 3 above.

Press “Ctrl+C” or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” to
exit the program.

![](/media/3b8f375f1e2f09e2f7f27b3cd4c13bc4.png)
