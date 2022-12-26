# Project 21：Relay

1. Introduction**：

In our daily life, we usually use communication to drive electrical
equipments, and sometimes we use switches to control electrical
equipments. If the switch is connected directly to the ac circuit,
leakage occurs and people are in danger. Therefore, from the
perspective of safety, we specially designed this relay module with
NO(normally open) end and NC(normally closed) end. In this project,
we will learn a relatively special and easy-to-use switch, which is
the relay module.

2. Components：

|                                    |                        |                         |                             |                        |
| ---------------------------------- | ---------------------- | ----------------------- | --------------------------- | ---------------------- |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| ESP32\*1                           | Breadboard\*1          | Relay Module\*1         | M-F Dupont Wires            | USB Cable\*1           |

3. Component knowledge：

**Relay:** It is an "automatic switch" that uses a small current to
control the operation of a large current.

Input voltage：3.3V-5V

Rated load：5A 250VAC (NO/NC) 5A 24VDC (NO/NC)

The rated load means that devices with dc voltage of 24V or AC voltage
of 250V can be controlled using 3.3V-5V microcontrollers.

**Schematic diagram of Relay：**

![](/media/be1c90d2b52fc2489590e3f702a087bf.emf)

4. Wiring Diagram：

![](/media/1741d3cb0405c740378ef7ef96df6072.png)

5. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
21：Relay”，and then double left-click“Project\_21\_Relay.py”.

![](/media/26d0543fe77e91b7f5d99c31b67963e2.png)

    from machine import Pin
    import time
    
    # create relay from Pin 15, Set Pin 15 to output 
    relay = Pin(15, Pin.OUT)
     
    # The relay is opened, COM and NO are connected on the relay, and COM and NC are disconnected.
    def relay_on():
        relay(1)
     
    # The relay is closed, the COM and NO on the relay are disconnected, and the COM and NC are connected.
    def relay_off():
        relay(0)
     
    # Loop, the relay is on for one second and off for one second
    while True:
        relay_on()
        time.sleep(1)
        relay_off()
        time.sleep(1)

6. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/2929f4abc3196645c4d5d2ed54542630.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the relay will cycle on and off, on for 1
second, off for 1 second.  At the same time, you can hear the sound of
the relay on and off, and you can also see the change of the indicator
light on the relay. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/4a5a3673874d5e5a942645b12c652621.png)
