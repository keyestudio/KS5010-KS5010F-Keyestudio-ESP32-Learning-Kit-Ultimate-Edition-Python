# Project 12：Active Buzzer

1.  **Introduction：**

Active buzzer is a sound component that is widely used as a sound
component for computers、printers、alarms、electronic toys and
phones、timers etc. It has an internal vibration source, just by
connecting to a 5V power supply, it can continuously buzz. In this
project, we will use ESP32 to control the active buzzer to beep.

2.  **Components：**

|                                    |                        |                                                  |                        |
| ---------------------------------- | ---------------------- | ------------------------------------------------ | ---------------------- |
| ![](/media/4b4f653a76a82a3b413855493cc58fba.png) |                        |
| ESP32\*1                           | Breadboard\*1          | Active buzzer\*1                                 |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| NPN transistor(S8050)\*1           | 1kΩResistor\*1         | Jumper Wires                                     | USB Cable\*1           |

**3. Component knowledge：**

![](/media/11ec5ddc982db9928341e858aab94652.png)

**Active buzzer:** Active buzzer inside has a simple oscillator circuit,
which can convert constant direct current into a certain frequency pulse
signal. Once active buzzer receives a high level, it will produce sound.
Passive buzzer is an internal without vibration source integrated
electronic buzzer, it must be driven by 2k to 5k square wave, rather
than a DC signal. The two buzzers are very similar in appearance, but
one buzzer with a green circuit board is a passive buzzer, while the
other buzzer with black tape is an active buzzer. Passive buzzers don't
have positive polarity, but active buzzers have. As shown below:

![](/media/0f9825969867ac2d65bb1a19ed0ad2ab.png)

**Transistor:**

![](/media/9197d4aff9356c585b7ef68e33a6881d.png)

Because the buzzer requires such large current that GPIO of ESP32 output
capability cannot meet the requirement, a transistor of NPN type is
needed here to amplify the current.

Transistor, the full name: semiconductor transistor, is a semiconductor
device that controls current. Transistorcan be used to amplify weak
signal, or works as a switch. It has three electrodes(PINs): base (b),
collector (c) and emitter (e). When there is current passing between
"be", "ce" will allow several-fold current (transistor magnification)
pass, at this point, transistor works in the amplifying area. When
current between "be" exceeds a certain value, "ce" will not allow
current to increase any longer, at this point, transistor works in the
saturation area. Transistor has two types as shown below: PNP and NPN,

![](/media/02dad9f2fcac0d7bfe4cc135d2301aa6.png)

PNP transistor NPN transistor

In our kit, the PNP transistor is marked with 8550, and the NPN
transistor is marked with 8050.

Based on the transistor's characteristics, it is often used as a switch
in digital circuits. As micro-controller's capacity to output current is
very weak, we will use transistor to amplify current and drive
large-current components.

When using NPN transistor to drive buzzer, we often adopt the following
method. If GPIO outputs high level, current will flow through R1, the
transistor will get conducted, and the buzzer will sound. If GPIO
outputs low level, no current flows through R1, the transistor will not
be conducted, and buzzer will not sound.

When using PNP transistor to drive buzzer, we often adopt the following
method. If GPIO outputs low level, current will flow through R1, the
transistor will get conducted, and the buzzer will sound. If GPIO
outputs high level, no current flows through R1, the transistor will not
be conducted, and buzzer will not sound.

![](/media/2a9755ec14ab58c67d7d8341601d8dbc.png)

4.  **Wiring diagram：**

![](/media/5c215684c8945622441478edb6f16e30.png)

Note: The buzzer power supply in this circuit is 5V. On a 3.3V power
supply, the buzzer can work, but will reduce the loudness.

5.  **Project code：**

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
12：Active Buzzer”, and then double left-click
“Project\_12\_Active\_Buzzer.py”.

![](/media/7e428db2af79108da6c6375abe2227eb.png)

    from machine import Pin
    import time
    
    buzzer = Pin(15, Pin.OUT)   # create buzzer object from Pin 15, Set Pin 15 to output
    
    try:
        while True:
            buzzer.value(1)    # Set buzzer turn on
            time.sleep(0.5) # Sleep 0.5s
            buzzer.value(0)    # Set buzzer turn off
            time.sleep(0.5) # Sleep 0.5s
    except:
        pass

6.  **Project result：**

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/74f70c214ee1ce51ffc05b9ba1ccc50a.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to
be executed and you'll see that the active buzzer beeps.
Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”
to exit the program.

![](/media/e603eb0f4295e5f34790e42454799fb9.png)
