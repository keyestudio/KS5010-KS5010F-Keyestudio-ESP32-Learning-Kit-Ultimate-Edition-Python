# Project 10：8×8 Dot-matrix Display

1.  **Introduction：**

Dot matrix display is an electronic digital display device that can
display information on machine, clocks, public transport departure
indicators and many other devices. In this project, we will use ESP32
control 8x8 LED dot matrix to display patterns.

2.  **Components：**

|                                    |                             |                        |
| ---------------------------------- | --------------------------- | ---------------------- |
| ![](/media/e380dd26e4825be9a768973802a55fe6.png)      |                        |
| ESP32\*1                           | Breadboard\*1               |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| 8\*8 dot matrix module\*1          | M-F Dupont Wires            | USB Cable\*1           |

3.  **Component knowledge：**

**8\*8 dot matrix module：**The 8\*8 dot matrix is composed of 64 LEDs,
and each LED is placed at the intersection of a row and a column. When
using the single chip microcomputer to drive an 8\*8 dot matrix, we need
16 digital ports in total, which greatly wastes the data of the single
chip microcomputer.To this end, we specially designed this module, using
the HT16K33 chip to drive an 8\*8 dot matrix, and only need to use the
I2C communication port of the MCU to control the 8\*8 dot matrix, which
greatly saving the MCU resources.

**Specifications of 8\*8 dot matrix module：**

Working voltage: DC 5V

Current: 200MA

Maximum power: 1W

**Schematic diagram of 8\*8 dot matrix module：**

![](/media/b04fe5e60695365a23644395aaef5085.png)

Some modules have three DIP switches that you can toggle at will. These
switches are used to set the I2C communication address, the setting
method is as follows. The module has fixed the communication address.
A0, A1 and A2 are connected to GND, and the address is 0x70.

|        |        |        |        |        |        |        |        |        |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| A0（1）  | A1（2）  | A2（3）  | A0（1）  | A1（2）  | A2（3）  | A0（1）  | A1（2）  | A2（3）  |
| 0（OFF） | 0（OFF） | 0（OFF） | 1（ON）  | 0（OFF） | 0（OFF） | 0（OFF） | 1（ON）  | 0（OFF） |
| 0X70   | 0X71   | 0X72   |        |        |        |        |        |        |
| A0（1）  | A1（2）  | A2（3）  | A0（1）  | A1（2）  | A2（3）  | A0（1）  | A1（2）  | A2（3）  |
| 1（ON）  | 1（ON）  | 0（OFF） | 0（OFF） | 0（OFF） | 1（ON）  | 1（ON）  | 0（OFF） | 1（ON）  |
| 0X73   | 0X74   | 0X75   |        |        |        |        |        |        |
| A0（1）  | A1（2）  | A2（3）  | A0（1）  | A1（2）  | A2（3）  |        |        |        |
| 0（OFF） | 1（ON）  | 1（ON）  | 1（ON）  | 1（ON）  | 1（ON）  |        |        |        |
| 0X76   | 0X77   |        |        |        |        |        |        |        |

4.  **Wiring diagram：**

![](/media/78a74a4a920791b492bcd398dc8dc82b.png)

5.  **Project code：**

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to
any location. For example, we save the codes in Disk(D) with the
path of “D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
10：8×8 Dot-matrix Display”. Select “ht16k33matrix.py” and
“ht16k33.py”，right-click your mouse to select “Upload to /”，wait
for “ht16k33matrix.py” and “ht16k33.py” to be uploaded to ESP32，and then
double left-click

“Project\_10\_8×8\_Dot\_Matrix\_Display.py”.

![](/media/b4d922fcc91b8b38c1c8115fd6e0ae45.png)

![](/media/f63f7f1977a8a737dabd96043bb9760b.png)

![](/media/04d33969c19b64eac0a6975f2bf1b307.png)

    # IMPORTS
    import utime as time
    from machine import I2C, Pin, RTC
    from ht16k33matrix import HT16K33Matrix
    
    # CONSTANTS
    DELAY = 0.01
    PAUSE = 3
    
    # START
    if __name__ == '__main__':
        i2c = I2C(scl=Pin(22), sda=Pin(21))
        display = HT16K33Matrix(i2c)
        display.set_brightness(2)
    
        # Draw a custom icon on the LED
        icon = b"\x00\x66\x00\x00\x18\x42\x3c\x00"
        display.set_icon(icon).draw()
        # Rotate the icon
        display.set_angle(0).draw()
        time.sleep(PAUSE)


6.  **Project result：**

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/614c69b10e2c02966595eacb82beec5d.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the 8\*8 dot matrix displays“Smiling face”
pattern. Press“Ctrl+C” or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”to exit the program.

![](/media/9df12595ad5847a06e300c5d2e51edb7.png)
