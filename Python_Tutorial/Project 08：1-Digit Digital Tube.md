# Project 08：1-Digit Digital Tube

1.  **Introduction：**

A 1-Digit 7-Segment Display is an electronic display device that
displays decimal numbers. It is widely used in digital clocks,
electronic meters, basic calculators and other electronic devices that
display digital information. Eventhough they may not look modern enough,
they are an alternative to more complex dot matrix displays and are easy
to use in limited light conditions and strong sunlight. In this project,
we will use ESP32 to control 1-Digit 7-segment display displays numbers.

2.  **Components：**

|                                    |                        |                        |                        |
| ---------------------------------- | ---------------------- | ---------------------- | ---------------------- |
| ![](/media/e380dd26e4825be9a768973802a55fe6.png) |                        |                        |
| ESP32\*1                           | Breadboard\*1          |                        |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| 1-Digit 7-Segment Display\*1       | 220Ω Resistor\*8       | Jumper Wires           | USB Cable\*1           |

**3. Component knowledge：**

![](/media/e44a0f27beec739ee13e68c04865989f.png)

**1-Digit 7-Segment Display principle:** Digital tube display is a
semiconductor light emitting device,its basic unit is a light-emitting
diode (LED). Thedigital tube display can be divided into 7-segment
display and 8-segment display according to the number of segments. The
8-segment display has one more LED unit than the 7-segment display (used
for decimal point display). Each segment of the 7-segment display is a
separate LED. According to the connection mode of the LED unit, the
digital tube can be divided into a common anode digital tube and a
common cathode digital tube.

In the common cathode 7-segment display, all the cathodes (or negative
electrodes) of the segmented LEDs are connected together, so you should
connect the common cathode to GND. To light up a segmented LED, you can
set its associated pin to“HIGH”.

In the common anode 7-segment display, the LED anodes (positive
electrodes) of all segments are connected together, so you should
connect the common anode to“+5V”. To light up a segmented LED, you can
set its associated pin to“LOW”.

![](/media/28fd057848fbe0e8c8e3362768e7aa44.png)

Each part of the digital tube is composed of an LED. So when you use it,
you also need to use a current limiting resistor. Otherwise, the LED
will be damaged. In this experiment, we use an ordinary common cathode
one-digit digital tube. As we mentioned above, you should connect the
common cathode to GND. To light up a segmented LED, you can set its
associated pin to“HIGH”.

**4.****Wiring diagram：**

Note: The direction of the 7-segment display inserted into the
breadboard is consistent with the wiring diagram, with one more point in
the lower right corner.

![](/media/631ee0861da60ed02d191de0e0e210d9.png)

![](/media/5f01d1eea2bb207f19dee4f437f93bc8.png)

**5.Project code：**

The digital display is divided into 7 segments, and the decimal point
display is divided into 1 segment. When certain numbers are displayed,
the corresponding segment will be lit. For example, when the number 1 is
displayed, segments b and c will be turned on.

Codes used in this tutorial are saved in”**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
08：1-Digit Digital Tube”, and double left-click
“Project\_08\_One\_Digit\_Digital\_Tube.py”.

![](/media/3be7059c709f19115166838408aee85f.png)

    from machine import Pin
    import time
    
    a = Pin(16, Pin.OUT)
    b = Pin(4, Pin.OUT)
    c = Pin(5, Pin.OUT)
    d = Pin(18, Pin.OUT)
    e = Pin(19, Pin.OUT)
    f = Pin(22, Pin.OUT)
    g = Pin(23, Pin.OUT)
    dp = Pin(17, Pin.OUT)
    
    pins = [Pin(id,Pin.OUT) for id in [16, 4, 5, 18, 19, 22, 23, 17]]
    
    def show(code):
        for i in range(0, 8):
            pins[i].value(~code & 1)
            code = code >> 1
    
    #Select code from 0 to 9
    mask_digits = [0xc0, 0xf9, 0xa4, 0xb0, 0x99, 0x92, 0x82, 0xf8,0x80, 0x90]
    for code in reversed(mask_digits):
        show(code)
        time.sleep(1)

6.  **Project result：**

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/7be4c73143be588035ba0e6d0e1c6fe4.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the 1-Digit 7-Segment Display will display
numbers from 9 to 0. Press “Ctrl+C” or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” to exit the
program.

![](/media/c84378a13a1f9b578d8edb57baaafd47.png)
