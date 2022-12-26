# Project 03：LED Flashing 

1.  **Introduction**：

In this project, we will show you the LED flashing effect. We use the
ESP32's digital pin to turn on the LED and make it flashing.

2.  **Components：**

|                                    |                        |                        |                        |
| ---------------------------------- | ---------------------- | ---------------------- | ---------------------- |
| ![](/media/e380dd26e4825be9a768973802a55fe6.png) |                        |                        |
| ESP32\*1                           | Breadboard\*1          |                        |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| Red LED\*1                         | 220Ω Resistor\*1       | Jumper Wire\*2         | USB Cable\*1           |

3.  **Wiring diagram：**

First, disconnect all power from the ESP32. Then build the circuit
according to the wiring diagram. After the circuit is built and verified
correct, connect the ESP32 to your computer using a USB cable.

**Note:** Avoid any possible short circuits (especially connecting 3.3V
and GND)\!

**WARNING:** A short circuit can cause high current in your circuit,
create excessive component heat and cause permanent damage to your
hardware\!

![](/media/0735997593c8858ad6441d8e9867206f.png)

Note:

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

4.  **Project code：**
    
Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to
any location. For example, we save the codes in Disk(D) with the
path of “D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Code running online:

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
03：LED Flashing”.

![](/media/aed4325f483f54272aba116d9d92190e.png)

Expand folder“Project 03：LED Flashing”and double left-click
“Project\_03\_LED\_Flashing.py” to open it. As shown in the
illustration below：

![](/media/e8d875ca48b359b3fe7df7f705dc97e4.png)

    from machine import Pin
    import time
    
    led = Pin(15, Pin.OUT)   # create LED object from Pin 15, Set Pin 15 to output
    
    try:
        while True:
            led.value(1)    # Set led turn on
            time.sleep(0.5) # Sleep 0.5s
            led.value(0)    # Set led turn off
            time.sleep(0.5) # Sleep 0.5s
    except:
        pass

Make sure the ESP32 has been connected to the computer.
Click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” and see what will
display in the“**Shell**”window.

![](/media/c78c222938d7337d595b3a753fdf702e.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”，the code starts to be
executed and you can see the LED is ON for 0.5 seconds and then OFF for
0.5 seconds, which repeats in an endless loop. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/d936f3f5a18081cd7539033991daf98b.png)

![](/media/2dcc6a55b77b4175b5175f717eb196c3.png)

**Note**: This is the code running online. If you disconnect USB cable
and repower ESP32 or press its reset button, the LED in the circuit
stops flashing and the following messages will be displayed in the
"Shell" window of Thonny:

![](/media/c2685b285afdb8a2f9e56ac70c874e98.png)

Code running offline（Upload the code to ESP32）：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”.

![](/media/df3715e5657c7edecff914d97f43b8de.png)

As shown below, right-click the
file“Project\_03\_LED\_Flashing.py”，select “**Upload to /**”to
upload the code to ESP32.

![](/media/010dbbff20232229cc92d885fda36d7d.png)

Upload“boot.py”in the same way.

![](/media/8cfeb1a3a4fba034c1d67ef272cb1118.png)

Press the reset button of ESP32 and you can see the LED is ON for 0.5
seconds and then OFF for 0.5 seconds, which repeats in an endless loop.

![](/media/2dcc6a55b77b4175b5175f717eb196c3.png)

**Note**：Codes here is run offline. If you want to stop running offline
and enter“**Shell**”, just click ![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”in Thonny.

![](/media/0fc03f7cc11e6d76447e1e670a1d77e8.png)
