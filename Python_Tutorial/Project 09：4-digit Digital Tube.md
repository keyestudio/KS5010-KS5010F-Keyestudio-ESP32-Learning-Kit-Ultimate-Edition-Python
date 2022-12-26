# Project 09：4-Digit Digital Tube

1.  **Introduction：**

A 4-digit 7-segment display is a very practical display device and it is
used for devices such as electronic clocks，score counters and the number
of people in the park. Because of the low price, easy to use, more and
more projects will use 4 Digit 7-segment display. In this project, we
use ESP32 control 4-digit 7-segment display to display four digits.

2.  **Components：**

|                                     |                             |                        |
| ----------------------------------- | --------------------------- | ---------------------- |
| ![](/media/e380dd26e4825be9a768973802a55fe6.png)      |                        |
| ESP32\*1                            | Breadboard\*1               |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| 4-digit 7-segment display Module\*1 | M-F Dupont Wires            | USB Cable\*1           |

3.  **Component knowledge：**

**TM1650** **4-digit 7-segment display：**It is a 12-pin 4-digit
7-segment display module with clock dots. The driver chip is TM1650
which only needs 2 signal lines to enable the microcontroller to control
the 4-digit 7-segment display. The control interface level can be 5V or
3.3V.

**Specifications of 4-bit 7-segment display module:**

Working voltage: DC 3.3V-5V

Maximum current: 100MA

Maximum power: 0.5W

**Schematic diagram of 4-digit 7-segment display module:**

![](/media/5f400887c90fc00098a3e77beca656ef.png)

4.  **Wiring diagram：**

![](/media/a7721c08ed3b73b21a997d43d2e3addd.png)

**5.** **Project code：**

Codes used in this tutorial are saved in”**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
09：4-Digit Digital Tube”. Select “TM1650.py”, right-click your mouse
to select “Upload to /”，wait for “TM1650.py” to be uploaded to ESP32，and
then double left-click “Project\_09\_Four\_Digit\_Digital\_Tube.py”.

![](/media/8137354f861e5abad5ffdc4a7deac5e6.png)

![](/media/d92d7622dcd0e72ca15ed8baf9198d2f.png)

    from machine import Pin, I2C
    from TM1650 import TM1650
    import time
    
    # Define IIC interfaces and frequencies
    i2c=I2C(0, scl=Pin(22),sda=Pin(21), freq=100000)
    
    display = TM1650(i2c)
    
    # Display the numbers 1111-9999 circulately
    while True:
        display.display(1111)
        time.sleep(1)
        display.display(2222)
        time.sleep(1)
        display.display(3333)
        time.sleep(1)
        display.display(4444)
        time.sleep(1)
        display.display(5555)
        time.sleep(1)
        display.display(6666)
        time.sleep(1)
        display.display(7777)
        time.sleep(1)
        display.display(8888)
        time.sleep(1)
        display.display(9999)
        time.sleep(1)


**6. Project result：**

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/7351c8d2713f1efe135b2baab468f5f9.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that 4-digit 7-segment display displays four
digits，and repeat these actions in an infinite loop. Press “Ctrl+C” or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” to exit the program.

![](/media/4a54190628b9af7ac90f10f6a1b0fde1.png)
