# Project 18：Small Fan

1. Introduction：

In hot summer, we need electric fans to cool us down, so in this
project, we will use ESP32 control 130 motor module and small fan blade
to make a small electric fan.

2. Components：

|                                    |                                                |                             |                                 |
| ---------------------------------- | ---------------------------------------------- | --------------------------- | ------------------------------- |
| ![](/media/b65d826ca481982fed0212dba2957c7c.jpeg)  |                                 |
| ESP32\*1                           | Breadboard\*1                                  | Battery Holder\*1           |                                 |
| ![](/media/a815c48437199c6ab79d74cd2d583de0.png)          |
| 130 Motor Module\*1                | Keyestudio bread board special power module\*1 | M-F Dupont Wires            | No.5 battery (self-provided)\*6 |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)                        |                             |                                 |
| Fan\*1                             | USB Cable\*1                                   |                             |                                 |

3. Component knowledge :

![](/media/75a9140bdb671783bb79a71ca76fae69.png)

**130 motor module:** The motor control module uses the HR1124S motor
control chip. which is a single-channel H-bridge driver chip for DC
motor.. The H-bridge driver part of the HR1124S uses low on-resistance
PMOS and NMOS power tubes. The low on-resistance ensure low power loss
of the chip and make the chip work safely for longer time In addition,
In addition, the HR1124S has low standby current and low static
operating current, which makes the HR1124S easy to use in toy solutions.

**Features:**

Working voltage: 5V

Working current: 200MA

Working power: 2W

Working temperature: -10℃\~ +50℃

**Schematic diagram of 130 motor module：**

![](/media/ee2deb2ed7ae310b953ff178aff3d6c1.emf)

**Keyestudio Breadboard Power Supply Module：**

![](/media/7ff03f4506988f1ce99c5757892fc6de.jpeg)

**Introduction:**

This breadboard power supply module is compatible with 5V and 3.3V,
which can be applied to MB102 breadboard. The module contains two
channels of independent control, powered by the USB all the way.

The output voltage is constant for the DC5V, and another way is powered
by DC6.5-12V, output controlled by the slide switch, respectively for
DC5V and DC3.3V.

If the other power supply is DC 6.5-12v, when the slide switch is
switched to +5V, the output voltages of the left and right lines of the
module are DC 5V. When the slide switch is switched to +3V, the output
voltage of the USB power supply terminal of the module is DC5V , and the
output voltage of the DC 6.5-12V power supply terminal of the other
power supply is DC3.3V.

**Specification:**

- Applied to MB102 breadboard;

- Input voltage：DC 6.5-12V or powered by USB;

- Output voltage：3.3V or 5V

- Max output current：\<700ma

- Up and down two channels of independent control, one of which can be
switched to 3.3V or 5V;

- Comes with two sets of DC output pins, easy for external use.

**4. Wiring Diagram：**

![](/media/83f622be72c1b5501ffeab7bd1caf421.png)

(Note: Connect the wires and then install a small fan blade on the
DC motor. )

<!-- end list -->

5. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
18：Small Fan”, and then double left-click“Project\_18\_
Small\_Fan.py”.

![](/media/e40393ea6293875df1ad979b94ecc894.png)

    from machine import Pin
    import time
    
    motor1a = Pin(15, Pin.OUT) # create motor1a object from Pin 15, Set Pin 15 to output
    motor1b = Pin(2, Pin.OUT) # create motor1b object from Pin 2, Set Pin 2 to output
    
    def forward():
        motor1a.value(1) # Set motor1a high
        motor1b.value(0) # Set motor1b low
    def backward():
        motor1a.value(0)
        motor1b.value(1)
    def stop():
        motor1a.value(0)
        motor1b.value(0)
    
    def test():
        forward() # motor forward
        time.sleep(5) #delay
        stop() # motor stop
        time.sleep(2)
        backward()# motor backward 
        time.sleep(5)
        stop()
        time.sleep(2)
        
    for i in range(5):
        test() 

6. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/fbded97dffdb5d431b017e4f07b1aef3.png)

External power supply and power on. Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run
current script”, the code starts to be executed and you'll see that the
small fan turns counterclockwise for 5 seconds and stops for 2 seconds,
and then turns clockwise for 5 seconds and stops for 2 seconds. Repeat
this rule for 5 times and then the small fan stops. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/b6815be3d6f0df0d8e47a235b1c6db56.png)
