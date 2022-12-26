# Project 02: Turn on LED

1.  **Introduction**：

In this project, we will show you how to light up the LED. We use the
ESP32's digital pin to turn on the LED so that the LED is lit up.

2.  **Components：**

|                                    |                        |                        |                        |
| ---------------------------------- | ---------------------- | ---------------------- | ---------------------- |
| ![](/media/e380dd26e4825be9a768973802a55fe6.png) |                        |                        |
| ESP32\*1                           | Breadboard\*1          |                        |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| Red LED\*1                         | 220Ω Resistor\*1       | Jumper Wire\*2         | USB Cable\*1           |

3.  **Component knowledge：**

**（1）LED:**

![](/media/081141eed6146deed2bfbd8e55a8465b.jpeg)

The LED is a semiconductor known as “light-emitting diode” ,which is an
electronic device made from semiconducting materials(silicon, selenium,
germanium, etc.). It has an anode and a cathode, the short lead is
cathode, which connects to GND; the long lead is anode, which connects
to3.3V or 5V.

![](/media/f70404aa49540fd7aecae944c7c01f83.jpeg)

**（2）Five-color ring resistor**

A resistor is an electronic component in a circuit that restricts or
regulates the flow current flow. On the left is the appearance of the
resistor and on the right is the symbol for the resistance in the
circuit . Its unit is(Ω). 1 mΩ= 1000 kΩ，1kΩ= 1000Ω.

![](/media/8a86f65cf820d08e8956daa70d1c4195.jpeg)
![](/media/f6079fe22518f0fc1b0c3a3b93a516a1.png)

We can use resistors to protect sensitive components, such as LED. The
strength of the resistance is marked on the body of the resistor with an
electronic color code. Each color code represents a number, and you can
refer to it in a resistance card.

\-Color 1 – 1st Digit.

\-Color 2 – 2nd Digit.

\-Color 3 – 3rd Digit.

\-Color 4 – Multiplier.

\-Color 5 – Tolerance.

![](/media/c3df005312cd9f6d4cdae6abf3cddb83.png)

In this kit, we provide three Five-color ring resistor with different
resistance values. Take three Five-color ring resistor as an example.

220Ω Resistor\*10

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

10KΩ Resistor\*10

![](/media/246cf3885dc837c458a28123885c9f7b.png)

1KΩ Resistor\*10

![](/media/19f5dfc51adfd79b04c3b164529767ed.png)

In the same voltage, there will be less current and more resistance. The
connection between current(I), voltage(V), and resistance(R) can be
expressed by the formula: I=U/R. In the figure below, if the voltage is
3V, the current through R1 is: I = U / R = 3 V / 10 KΩ= 0.0003A= 0.3mA.

![](/media/b3eec552e4dfad361833730698621776.png)

Don’t connect a low resistance directly to the two poles of the power
supply. as this will cause excessive current to damage the electronic
components. Resistors do not have positive and negative poles.

**（3）Breadboard**

Breadboards are used to build and test circuits quickly before
completing any circuit design. There are many holes in the breadboard
that can be inserted into circuit components such as integrated circuit
board and resistors. A typical breadboard is shown below：

![](/media/612c1381811b2d780d5f6ed6a7ec3701.png)

The breadboard has strips of metal , which run underneath the board and
connect the holes on the top of the board. The metal strips are laid out
as shown below. Note that the top and bottom rows of holes are connected
horizontally，while the remaining holes are connected vertically.

![](/media/b45e70b961537035c85878b73d371725.png)

The first two rows (top) and the last two rows (bottom) of the
breadboard are used for the positive pole (+) and negative pole (-) of
the power supply respectively. The conductive layout of the breadboard
is shown in the figure below:

![](/media/d5478bd5eac558252cbc235479d979eb.png)

When we connect DIP (Dual In-line Packages) components, such as
integrated circuits, microcontrollers, chips and so on, we can see that
a groove in the middle isolates the middle part, so the top and bottom
of the groove is not connected. DIP components can be connected as shown
in the following diagram:

![](/media/50caf14e911c4244779e99445c658db6.png)

![](/media/9b66ae2199e77fbc99b7b278dac0b567.png)

4)  **[Power](javascript:;) [Supply](javascript:;)**

The ESP32 needs 3.3V-5V power supply. In this project, we connected
the ESP32 to the computer by using a USB cable.

![](/media/56053f7126905c6def63919c661d5c0a.jpeg)

4.  **Wiring diagram：**

First, disconnect all power from the ESP32. Then build the circuit
according to the wiring diagram. After the circuit is built and verified
correct, connect the ESP32 to your computer by using a USB cable.

**Note:** Be careful to avoid short circuit when connecting 3.3V and
GND\!

**WARNING:** A short circuit can cause high current in your circuit,
create excessive component heat and cause permanent damage to your
hardware\!

![](/media/0735997593c8858ad6441d8e9867206f.png)

Note:

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

5.  **Project code：**
    
Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to
any location. For example, we save the codes in Disk(D) with the
path of “D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Code running online:

Open “Thonny”，click “This computer”→“D:”→“2. Python Projects”→“Project
02：Turn On LED”.

![](/media/150fef13c4692cdb7f8f794aefe98bc9.png)

Expand folder“Project 02：Turn On LED”and double
left-click“Project\_02\_Turn\_On\_LED.py” to open it. As shown in the
illustration below：

![](/media/0d33b50cd534eb40eae8236b33d87fb9.png)

    from machine import Pin
    import time
    
    led = Pin(15, Pin.OUT)   # create LED object from Pin 15, Set Pin 15 to output
    
    led.value(1)    # Set led turn on
    


Make sure the ESP32 has been connected to the computer.
Click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” and see what will
display in the“**Shell**” window.

![](/media/2bd17f711463fca2f9142e5d9df692e8.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”，the code starts to be
executed and the LED in the circuit lit up. Press “Ctrl+C” or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” to exit the program.

![](/media/05bcd1d12a4c26f828e0f543d9a821d2.png)

![](/media/77dec960e108229b6d97b4af9a2db902.png)

**Note**: This is the code running online. If you disconnect USB cable
and repower ESP32 or press its reset button, LED is not bright and the
following messages will be displayed in the "**Shell**" window of
Thonny:

![](/media/379994d951e5fe47c618c99b56515759.png)

Code running offline（Upload the code to ESP32）：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”.

![](/media/eaaffbbb351874eb5c585ab7c196dec6.png)

As shown below, right-click the
file“Project\_02\_Turn\_On\_LED.py”，select “**Upload to /**”to
upload the code to ESP32.

![](/media/16334cff6440b3c4ef7d57c255a5fd95.png)

Upload“boot.py”in the same way.

![](/media/5e0ff1eb1d1d14394bebd6a73c96e987.png)

Press the reset button of ESP32 and you can see LED is ON .

![](/media/77dec960e108229b6d97b4af9a2db902.png)

**Note**：Codes here is run offline. If you want to stop running offline
and enter“**Shell**”, just click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”in Thonny.

![](/media/61c2b113ea1bc2e2e52cd2dada6c28d8.png)
