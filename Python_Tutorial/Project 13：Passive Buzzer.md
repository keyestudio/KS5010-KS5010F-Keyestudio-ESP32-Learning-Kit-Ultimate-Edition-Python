# Project 13：Passive Buzzer

1. Introduction:

In a previous project, we studied an active buzzer, which can only make
a sound and may make you feel very monotonous. In this project, we will
learn a passive buzzer and use the ESP32 control it to work. Unlike the
active buzzer, the passive buzzer can emit sounds of different
frequencies.

2. Components：

|                                    |                        |                                                |                        |
| ---------------------------------- | ---------------------- | ---------------------------------------------- | ---------------------- |
| ![](/media/d1ea1bb2b2749820cab389d5b85b838b.png) |                        |
| ESP32\*1                           | Breadboard\*1          | Passive Buzzer \*1                             |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| NPN transistor(S8050)\*1           | 1kΩResistor\*1         | Jumper Wires                                   | USB Cable\*1           |

3. Component knowledge：

![](/media/8d0020e53824072cbe9d4f7d2f8acb4f.png)

**Passive buzzer:** A passive buzzer is an integrated electronic buzzer
with no internal vibration source and it has to be driven by 2K-5K
square waves, not DC signals. The two buzzers are very similar in
appearance, but one buzzer with a green circuit board is a passive
buzzer and the other buzzer with black tape is an active buzzer. Passive
buzzers cannot distinguish between positive polarity while active
buzzers can.

![](/media/fc42c5ed014609ff0b290ee5361bb2fd.png)

**Transistor:** Please refer to Project 12.

4. Wiring diagram:

![](/media/9c12d89ce3f10c838e63f1334f41fc9e.png)

5. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
13：Passive Buzzer”, and then double left-click
“Project\_13\_Passive\_Buzzer.py”.

![](/media/fccdd67efcf74c9f511b3ec1a5e297a9.png)

    from machine import Pin
    import time
    
    #Initialize the passive buzzer
    buzzer = Pin(15,Pin.OUT)
    
    #Simulate two different frequencies
    while True:
        #Output 500HZ frequency sound
        for i in range(80):
            buzzer.value(1)
            time.sleep(0.001)
            buzzer.value(0)
            time.sleep(0.001)
        #Output 250HZ frequency sound
        for i in range(100):
            buzzer.value(1)
            time.sleep(0.002)
            buzzer.value(0)
            time.sleep(0.002)

6. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”.

![](/media/eba3a2bbd42baec5030d1b23e6f52f72.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the passive buzzer sounds alarm.
Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to
exit the program.

![](/media/5d4bc5fbcacd652709aef97bbe9e7f4b.png)
