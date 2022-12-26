# Project 06: RGB LED

**1.Introduction：**

![](/media/94bdff69e438989d8e0934e57f2e5c00.png)

RGB is composed of three colors (red, green and blue),which can emit
different colors of light by mixing these three basic colors.

In this project, we will introduce the RGB and show you how to use ESP32
to control the RGB to emit different color light .RGB is pretty basic,
but it’s also a great way to learn the fundamentals of electronics and
coding.

2.  **Components：**

|                                    |                        |                        |                        |
| ---------------------------------- | ---------------------- | ---------------------- | ---------------------- |
| ![](/media/e380dd26e4825be9a768973802a55fe6.png) |                        |                        |
| ESP32\*1                           | Breadboard\*1          |                        |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| RGB LED\*1                         | 220Ω Resistor\*3       | Jumper Wires           | USB Cable\*1           |

**3.** **Component knowledge：**

Most monitors adopt the RGB color standard, and all colors on a computer
screen are a mixture of red, green and blue in varying proportions.

![](/media/8bf1339719a922f2fbc1e01a4347b4ab.png)

This RGB LED has 4 pins, each color (red, green, blue) and a common
cathode,To change its brightness, we can use the PWM of the ESP32 pins,
which can give different duty cycle signals to the RGB to produce
different colors of light.

If we use three 10-bit PWM to control the RGB, in theory, we can create
2 <sup>10</sup>\*2<sup>10</sup>\*2<sup>10</sup> = 1,073,741,824(1
billion) colors through different combinations.

4.  **Wiring diagram：**

![](/media/f3deb3502985ac8d66e99e4f27b3de1e.png)

**Note:**

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

5.  **Project** **code：**

Codes used in this tutorial are saved in”**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to
any location. For example, we save the codes in Disk(D) with the
path of “D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
06：RGB LED”, and double left-click “Project\_06\_RGB\_LED.py”.

![](/media/fdd3d2415740555f8814354b0537fdbc.png)

    # import Pin, PWM and Random function modules.
    from machine import Pin, PWM
    from random import randint
    import time
    
    #Configure ouput mode of GPIO15, GPIO2 and GPIO0 as PWM output and PWM frequency as 10000Hz.
    pins = [0, 2, 15]
    
    pwm0 = PWM(Pin(pins[0]),10000)  
    pwm1 = PWM(Pin(pins[1]),10000)
    pwm2 = PWM(Pin(pins[2]),10000)
    
    #define a function to set the color of RGBLED.
    def setColor(r, g, b):
        pwm0.duty(1023-r)
        pwm1.duty(1023-g)
        pwm2.duty(1023-b)
        
    try:
        while True:
            red   = randint(0, 1023) 
            green = randint(0, 1023)
            blue  = randint(0, 1023)
            setColor(red, green, blue)
            time.sleep_ms(200)
    except:
        pwm0.deinit()
        pwm1.deinit()
        pwm2.deinit()

6.  **Project result：**

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/fa525eea2405bb70e8d92c436b32852d.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that RGB begins to display random colors. Press
“Ctrl+C” or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” to exit
the program.

![](/media/d275633838f264432dae51e15f7e59bc.png)
