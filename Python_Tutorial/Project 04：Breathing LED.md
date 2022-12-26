# Project 04: Breathing Led

1.  **Introduction：**

In previous studies, we know that LEDs have on/off state, so how to
enter the intermediate state? How to output an intermediate state to
make the LED half bright? That's what we're going to learn.

Breathing light, that is, LED is turned from off to on gradually, and
gradually from on to off, just like "breathing". So, how to control the
brightness of a LED? We will use ESP32’s PWM to achieve this target.

2.  **Components：**

|                                    |                        |                        |                        |
| ---------------------------------- | ---------------------- | ---------------------- | ---------------------- |
| ![](/media/e380dd26e4825be9a768973802a55fe6.png) |                        |                        |
| ESP32\*1                           | Breadboard\*1          |                        |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| Red LED\*1                         | 220Ω Resistor\*1       | Jumper Wire\*2         | USB Cable\*1           |

3.  **Component knowledge：**

![](/media/6549bdbfd4e7b6b2b341012105d655e8.png)

**Analog & Digital:**

An Analog Signal is a continuous signal in both time and value. On the
contrary, a Digital Signal or discrete time signal is a time series
consisting of a sequence of quantities. Most signals in life are analog
signals. A familiar example of an Analog Signal would be how the
temperature throughout the day is continuously changing and could not
suddenly change instantaneously from 0℃ to 10℃. However, Digital Signals
can instantaneously change in value. This change is expressed in numbers
as 1 and 0 (the basis of binary code). Their differences can more easily
be seen when compared when graphed as below.

![](/media/4bdf6127e563b453a1fd8953b4ebb277.png)

In practical application, we often use binary as the digital signal,
that is a series of 0’s and 1’s. Since a binary signal only has two
values (0 or 1), it has great stability and reliability. Lastly, both
analog and digital signals can be converted into the other.

**PWM：**

PWM, Pulse-Width Modulation, is a very effective method for using
digital signals to control analog circuits. Common processors cannot
directly output analog signals. PWM technology makes it very convenient
to achieve this conversion (translation of digital to analog signals).

PWM technology uses digital pins to send certain frequencies of square
waves, that is, the output of high levels and low levels, which
alternately last for a while. The total time for each set of high levels
and low levels is generally fixed, which is called the period (Note: the
reciprocal of the period is frequency). The time of high level outputs
are generally called “pulse width”, and the duty cycle is the percentage
of the ratio of pulse duration, or pulse width (PW) to the total period
(T) of the waveform.

The longer the output of high levels last, the longer the duty cycle and
the higher the corresponding voltage in the analog signal will be. The
following figures show how the analog signal voltages vary between
0V-3V3 (high level is 3V3) corresponding to the pulse width 0%-100%:

![](/media/a439e1bd8a4578b43b7188c821d58594.jpeg)

The longer the PWM duty cycle is, the higher the output power will be.
Now that we understand this relationship, we can use PWM to control the
brightness of an LED or the speed of DC motor and so on. It is evident
from the above that PWM is not real analog, and the effective value of
the voltage is equivalent to the corresponding analog. so, we can
control the output power of the LED and other output modules to achieve
different effects.

**ESP32 and PWM:**

The ESP32 PWM controller has 8 independent channels, each of which can
independently control frequency, duty cycle, and even accuracy. Unlike
traditional PWM pins, the PWM output pins of ESP32 are configurable and
they can be configured to PWM.

4.  **Wiring diagram：**

![](/media/0735997593c8858ad6441d8e9867206f.png)

**Note:**

How to connect a LED

![](/media/42ff6f405dfa128593827de5aa03e94b.png)

How to identify the 220Ω Five-color ring resistor

![](/media/55c0199544e9819328f6d5778f10d7d0.png)

**5. Project code：**

The design of this project makes the GP15 output PWM, and the pulse
width gradually increases from 0% to 100%, and then gradually decreases
from 100% to 0%.

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
04：Breathing Led”, and double left-click
“Project\_04\_Breathing\_LED.py”.

![](/media/36ed8d4dadbfa227747fb2a2040c1fe6.png)

    import time
    from machine import Pin,PWM
    
    #The way that the ESP32 PWM pins output is different from traditionally controllers.
    #It can change frequency and duty cycle by configuring PWM’s parameters at the initialization stage.
    #Define GPIO15’s output frequency as 10000Hz and its duty cycle as 0, and assign them to PWM.
    pwm =PWM(Pin(15,Pin.OUT),10000,0)
    
    try:
        while True:
    #The range of duty cycle is 0-1023, so we use the first for loop to control PWM to change the duty
    #cycle value,making PWM output 0% -100%; Use the second for loop to make PWM output 100%-0%.  
            for i in range(0,1023):
                pwm.duty(i)
                time.sleep_ms(1)
                
            for i in range(0,1023):
                pwm.duty(1023-i)
                time.sleep_ms(1)  
    except:
    #Each time PWM is used, the hardware Timer will be turned ON to cooperate it. Therefore, after each use of PWM,
    #deinit() needs to be called to turned OFF the timer. Otherwise, the PWM may fail to work next time.
        pwm.deinit()

**6. Project result：**

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/89485986d9a0a7c5efcfd4b0356440f5.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the LED is turned from ON to OFF and then
back from OFF to ON gradually like breathing. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” to exit the program.

![](/media/62c772c3c9dadbfc1b3b720dab647f8e.png)

![](/media/3673c95868f245ee28365de8e51d2ced.png)
