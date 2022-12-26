# Project 22：Dimming Light

1. Introduction：

A potentiometer is a three-terminal resistor with sliding or rotating
contacts that forms an adjustable voltage divider. It works by changing
the position of the sliding contacts across a uniform resistance. In the
potentiometer, the entire input voltage is applied across the whole
length of the resistor, and the output voltage is the voltage drop
between the fixed and sliding contact.

In this project, we will learn how to use ESP32 to read the values of
the potentiometer, and make a dimming lamp with LED.

2. Components：

|                                    |                        |                          |                             |
| ---------------------------------- | ---------------------- | ------------------------ | --------------------------- |
| ![](/media/ef77f5a64c382157fc2dea21ec373fef.png) |
| ESP32\*1                           | Breadboard\*1          | Potentiometer\*1         | Red LED\*1                  |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)   |                             |
| 220ΩResistor\*1                    | Jumper Wires           | USB Cable\*1             |                             |

3. Component knowledge：

![](/media/03ab81e8b4f09287d2781ef0fd297f85.png)

**Adjustable potentiometer:** It is a kind of resistor and an analog
electronic component, which has two states of 0 and 1(high level and low
level). The analog quantity is different, its data state presents a
linear state such as 1 \~ 1024。

**ADC :** An ADC is an electronic integrated circuit used to convert
analog signals such as voltages to digital or binary form consisting of
1s and 0s. The range of our ADC on ESP32 is 12 bits, that means the
resolution is 2^12=4096, and it represents a range (at 3.3V) will be
divided equally to 4096 parts. The rage of analog values corresponds to
ADC values. So the more bits the ADC has, the denser the partition of
analog will be and the greater the precision of the resulting
conversion.

![](/media/f6c45550f4adf8373d7f1d01daec2c64.png)

Subsection 1: the analog in rang of 0V---3.3/4095 V corresponds to
digital 0;

Subsection 2: the analog in rang of 3.3/4095 V---2\*3.3 /4095V
corresponds to digital 1;

…

The following analog will be divided accordingly.

The conversion formula is as follows:

**DAC：**The reversing of this process requires a DAC, Digital-to-Analog
Converter. The digital I/O port can output high level and low level (0
or 1), but cannot output an intermediate voltage value. This is where a
DAC is useful. ESP32 has two DAC output pins with 8-bit accuracy, GPIO25
and GPIO26, which can divide VCC

(here is 3.3V) into 2^8=256 parts. For example, when the digital
quantity is 1, the output voltage value is 3.3/256 \*1 V, and when the
digital quantity is 128, the output voltage value is 3.3/256
\*128=1.65V, the higher the accuracy of DAC, the higher the accuracy of
output voltage value will be.

The conversion formula is as follows:

**ADC on ESP32：**

ESP32 has 16 pins can be used to measure analog signals. GPIO pin
sequence number and analog pin definition are shown in the following
table：

|                         |                       |
| ----------------------- | --------------------- |
| **ADC number in ESP32** | **ESP32 GPIO number** |
| **ADC0**                | **GPIO 36**           |
| **ADC3**                | **GPIO 39**           |
| **ADC4**                | **GPIO 32**           |
| **ADC5**                | **GPIO33**            |
| **ADC6**                | **GPIO34**            |
| **ADC7**                | **GPIO 35**           |
| **ADC10**               | **GPIO 4**            |
| **ADC11**               | **GPIO0**             |
| **ADC12**               | **GPIO2**             |
| **ADC13**               | **GPIO15**            |
| **ADC14**               | **GPIO13**            |
| **ADC15**               | **GPIO 12**           |
| **ADC16**               | **GPIO 14**           |
| **ADC17**               | **GPIO27**            |
| **ADC18**               | **GPIO25**            |
| **ADC19**               | **GPIO26**            |

**DAC on ESP32：**

ESP32 has two 8-bit digital analog converters to be connected to GPIO25
and GPIO26 pins, respectively, and it is immutable. As shown in the
following table：

|                         |                 |
| ----------------------- | --------------- |
| **Simulate pin number** | **GPIO number** |
| **DAC1**                | **GPIO25**      |
| **DAC2**                | **GPIO26**      |

4.  **Read the ADC value, DAC value and voltage value of the
potentiometer：**

We connect the potentiometer to the analog IO port of ESP32 to read the
ADC value, DAC value and voltage value of the potentiometer, please
refer to the wiring diagram below：

![](/media/0cda3256a0930404abc097ec8ffa3013.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
22：Dimming Light”，and then double left-click
“Project\_22.1\_Read\_Potentiometer\_Analog\_Value.py”.

![](/media/06ac796108af1e3f93eb1cea8519421e.png)

    # Import Pin, ADC and DAC modules.
    from machine import ADC,Pin,DAC
    import time
    
    # Turn on and configure the ADC with the range of 0-3.3V 
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_12BIT)
    
    # Read ADC value once every 0.1seconds, convert ADC value to DAC value and output it,
    # and print these data to “Shell”. 
    try:
        while True:
            adcVal=adc.read()
            dacVal=adcVal//16
            voltage = adcVal / 4095.0 * 3.3
            print("ADC Val:",adcVal,"DACVal:",dacVal,"Voltage:",voltage,"V")
            time.sleep(0.1)
    except:
        pass

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/0cd6434f99036eae34e08cf41e077e02.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the "Shell" window of Thonny IDE will print
the ADC value, DAC value and voltage value of the potentiometer, turn
the potentiometer handle, the ADC value and voltage value will change.
Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to
exit the program.

![](/media/ec206f4a6e39e73ca1090463b0fed249.png)

![](/media/65e6848785b8e09c731df4dd1f68a3a0.png)

5. Wiring diagram of the dimming lamp：

In the previous step, we read the ADC value, DAC value and voltage value
of the potentiometer. Now we need to convert the ADC value of the
potentiometer into the brightness of the LED to make a lamp that can
adjust the brightness.The wiring diagram is as follows:

![](/media/3396bd77169711de6e15da73f14c8afb.png)

6. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
22：Dimming Light”，and then double
left-click“Project\_22.2\_Dimming\_Light.py”.

![](/media/38a314cdea1135d7b329ffd722ef2946.png)

    from machine import Pin,PWM,ADC
    import time
    
    pwm =PWM(Pin(15,Pin.OUT),1000)
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_10BIT)
    
    try:
        while True:
            adcValue=adc.read()
            pwm.duty(adcValue)
            print(adc.read())
            time.sleep_ms(100)
    except:
        pwm.deinit()

7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/044b76a8bd7db21d2d7181fd6278d3cb.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that turn the potentiometer handle and the
brightness of the LED will change accordingly. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/bf01f65e47f89542d2d8d4c52410d74d.png)

![](/media/eca30dead3f4923afa0dcb0306db2319.jpeg)
