# Project 28：Rocker control light

1. Introduction：

The rocker module is a component with two analog inputs and one digital
input. It is widely used in areas such as game operation、robot control
and drone control. In this project, we use ESP32 and a joystick module
to control RGB, so that you can have a deeper understanding of the
principle and operation of the joystick module in practice. 

2. Components：

|                                    |                        |                         |                        |                             |
| ---------------------------------- | ---------------------- | ----------------------- | ---------------------- | --------------------------- |
| ![](/media/d087b123748cbfb8ed9f517150db71c5.png) |                        |                             |
| ESP32\*1                           | Breadboard\*1          | Rocker Module\*1        |                        |                             |
| ![](/media/f1aed48e2c02214415853ad2358f3744.png) |
| RGB LED\*1                         | 220ΩResistor\*3        | Jumper Wires            | USB Cable\*1           | M-F Dupont Wires            |

3. Component knowledge：

![](/media/d087b123748cbfb8ed9f517150db71c5.png)

**Rocker module:** It mainly uses PS2 joystick components. In fact, the
joystick module has 3 signal terminal pins, which simulate a
three-dimensional space. The pins of the joystick module are GND, VCC,
and signal terminals (B, X, Y). The signal terminals X and Y simulate
the X-axis and Y-axis of the space. When controlling, the X and Y signal
terminals of the module are connected to the analog port of the
microcontroller. The signal terminal B simulates the Z axis of the
space, it is generally connected to the digital port and used as a
button.

VCC is connected to the microcontroller power output VCC (3.3V or 5V),
GND is connected to the microcontroller GND, the voltage in the original
state is about 1.65V or 2.5V. In the X-axis direction, when moving in
the direction of the arrow, the voltage value increases, and the maximum
voltage can be reached. Moving in the opposite direction of the arrow,
the voltage value gradually decreases to the minimum voltage. In the
Y-axis direction, the voltage value decreases gradually as it moves in
the direction of the arrow on the module, decreasing to the minimum
voltage. As the arrow is moved in the opposite direction, the voltage
value increases and can reach the maximum voltage. In the Z-axis
direction, the signal terminal B is connected to the digital port and
outputs 0 in the original state and outputs 1 when pressed. In this way,
we can read the two analog values and the high and low level conditions
of the digital port to determine the operating status of the joystick on
the module.

**Features:**

Input Voltage：DC 3.3V \~ 5V.

Output Signal：X/Y dual axis analog value +Z axis digital signal.

[Range](javascript:;) [of](javascript:;) [Application](javascript:;)：Suitable
for control point coordinate movement in plane as well as control of two
degrees of freedom steering gear, etc.  

[product](javascript:;) [feature](javascript:;)s：Exquisite appearance,
joystick feel superior, simple operation, sensitive response, long
service life.

4. Read the value of the Rocker Module：

We must use ESP32’s analog IO port to read the value from the X/Y pin of
the rocker module and use the digital IO port to read the digital signal
of the button. Please connect the wires according to the wiring diagram
below：

![](/media/b611755eacc4c603e6c0555aced929cb.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
28：Rocker control light”, and then double left-click
“Project\_28.1\_Read\_Rocker\_Value.py”.

![](/media/77bd65288038e4677fe27eb4cd3afb11.png)

    from machine import Pin, ADC
    import time
    # Initialize the joystick module (ADC function)
    rocker_x=ADC(Pin(36))
    rocker_y=ADC(Pin(39))
    button_z=Pin(14,Pin.IN,Pin.PULL_UP)
    
    # Set the acquisition range of voltage of the two ADC channels to 0-3.3V,
    # and the acquisition width of data to 0-4095.
    rocker_x.atten(ADC.ATTN_11DB)
    rocker_y.atten(ADC.ATTN_11DB)
    rocker_x.width(ADC.WIDTH_12BIT)
    rocker_y.width(ADC.WIDTH_12BIT)
     
    # In the code, configure Z_Pin to pull-up input mode.
    # In loop(), use Read () to read the value of axes X and Y 
    # and use value() to read the value of axis Z, and then display them.
    while True:
        print("X,Y,Z:",rocker_x.read(),",",rocker_y.read(),",",button_z.value())
        time.sleep(0.5)

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/71e553d768f7ac5ec5a58e832daa2cb2.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the "Shell" window of Thonny IDE will print
the analog and digital values of the current joystick. Moving the
joystick or pressing it will change the analog and digital values in
"Shell". Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”to exit the program.

![](/media/17c6d800311f6c8d24f247a977239df3.png)

![](/media/06a9de681779df5cfc7e6bc24a928a3a.jpeg)

![](/media/6e7dd18099836222c5237c9e0e659539.png)

5. Wiring diagram of Rocker control light：

We just read the value of the rocker module, we need to do something
with the rocker module and RGB here, Follow the diagram below for
wiring：

![](/media/4ec49b488fedf216d03e49f83bc8443a.png)

6. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
28：Rocker control light”，and then double left-click
“Project\_28.2\_Rocker\_Control\_Light.py”.

![](/media/d96da59403c3e18ac63579fbd09628f0.png)

    from machine import Pin, ADC,PWM 
    import time
    #Set RGB light interface and frequency
    rgb_r = PWM(Pin(4))
    rgb_g = PWM(Pin(0))
    rgb_b = PWM(Pin(2))
    rgb_b.freq(1000)
    rgb_r.freq(1000)
    rgb_g.freq(1000)
    #Set rocker pin
    rocker_x=ADC(Pin(36))
    rocker_y=ADC(Pin(39))
    # Set the acquisition range of voltage of the two ADC channels to 0-3.3V,
    # and the acquisition width of data to 0-4095.
    rocker_x.atten(ADC.ATTN_11DB)
    rocker_y.atten(ADC.ATTN_11DB)
    rocker_x.width(ADC.WIDTH_12BIT)
    rocker_y.width(ADC.WIDTH_12BIT)
    
    while True:
        y = rocker_y.read()#Get Y value of rocker
        x = rocker_x.read()#Get X value of rocker
        if x < 1000:    #left
            rgb_b.duty(0)
            rgb_r.duty(1023)
            rgb_g.duty(0)
        elif x > 3000:    #right
            rgb_b.duty(0)
            rgb_r.duty(0)
            rgb_g.duty(1023)
        elif y < 1000:    #down
            rgb_b.duty(1023)
            rgb_r.duty(0)
            rgb_g.duty(0)
        elif y > 3000:    #up
            rgb_b.duty(1023)
            rgb_r.duty(1023)
            rgb_g.duty(1023)
        time.sleep(0.01)

7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/4f9d5c383ac44a0a911eb378b114174c.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that ①If the rocker is moved to the far left in
the X direction, the RGB light turns red. ② If the rocker is moved to
the far right in the X direction, the RGB light turns green. ③If the
rocker is moved to the up in the Y direction, the RGB light turns white.
④If the rocker is moved to the down in the Y direction, the RGB light
turns blue. Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”to exit the program.

![](/media/1e86592d0b4e70cd1cc98db6ccd24d05.png)

![](/media/9c2d0d8777200827b16c49b752d45c4c.jpeg)
