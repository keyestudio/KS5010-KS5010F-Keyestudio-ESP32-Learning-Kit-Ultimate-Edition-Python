# Project 11：74HC595N Control 8 LEDs 

1.  **Introduction：**

In previous projects, we learned how to light up an LED.

With only 32 IO ports on ESP32, how do we light up a lot of
leds? Sometimes it is possible to run out of pins on the ESP32, and you
need to extend it with the shift register.You can use the 74HC595N chip
to control 8 outputs at a time, taking up only a few pins on your
microcontroller. In addition, you can also connect multiple registers
together to further expand the output. In this project, we will use
ESP32、74HC595 chip and LED to make a flowing water light to understand
the function of the 74HC595 chip.

2.  **Components：**

|                                    |                             |                        |                        |
| ---------------------------------- | --------------------------- | ---------------------- | ---------------------- |
| ![](/media/c801a7baee258ff7f5f28ac6e9a7097b.png) |
| ESP32\*1                           | Breadboard\*1               | 74HC595N chip\*1       | Jumper Wires           |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |                        |
| 220ΩResistor\*8                    | Red LED\*8                  | USB Cable\*1           |                        |

3.  **Component knowledge：**

![](/media/6921c6d60135e072ed4bd24564ec4a6d.png)

**74HC595N Chip:** The 74HC595 chip is used to convert serial data into
parallel data. A 74HC595 chip can convert the serial data of one byte
into 8 bits, and send its corresponding level to each of the 8 ports
correspondingly. With this characteristic, the 74HC595 chip can be used
to expand the IO ports of an ESP32. At least 3 ports are required to
control the 8 ports of the 74HC595 chip.

![](/media/858b189f06ad68afe051b15043b2affd.png)

The ports of the 74HC595 chip are described as follows ：

<table>
<tbody>
<tr class="odd">
<td>Pin 13--OE</td>
<td><p>Enable output,</p>
<p>When this pin is in high level, Q0-Q7 is in high resistance state.</p>
<p>When this pin is in low level, Q0-Q7 is in output mode.</p></td>
</tr>
<tr class="even">
<td>Pin 14---SI</td>
<td>Serial data Input, only enter one bit at a time, so you can enter eight consecutive times to form one byte.</td>
</tr>
<tr class="odd">
<td>Pin 10---SCLR</td>
<td>Remove shift register: When this pin is in low level, the content in shift register will be cleared.. In this experiment, we connect VCC to maintain a high level.</td>
</tr>
<tr class="even">
<td>Pin 11---SCK</td>
<td>Serial shift clock: when its electrical level is rising, serial data input register will do a shift.</td>
</tr>
<tr class="odd">
<td>Pin 12---RCK</td>
<td>Parallel Update Output: when its electrical level is rising, it will update the parallel data output. In this case, the data is output from ports Q0 to Q7 in parallel</td>
</tr>
<tr class="even">
<td>Pin 9---SQH</td>
<td>Serial data output: it can be connected to more 74HC595 in series.</td>
</tr>
<tr class="odd">
<td>Q0--Q7(Pin 15，Pin 1-7)</td>
<td>Parallel data output, can directly control the 8 segments of the digital tube.</td>
</tr>
</tbody>
</table>

**4.** **Wiring diagram：**

Note: Note the orientation in which the 74HC595N chip is inserted.

![](/media/a6d03617539b70d6d69fa7e9acb25be9.png)

![](/media/11a03579b6cf94599f00554bfe014a3b.png)

**5.** **Project code：**

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path
of“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
11：74HC595N Control 8 LEDs”. Select“my74HC595.py”, right click your
mouse to select“Upload to /”，wait for“my74HC595.py”to be uploaded to
ESP32, and then double left-click
“Project\_11\_74HC595N\_Controls\_8\_LEDs.py”.

![](/media/10e5ce5f809b1718a0a92d0bf90ecd3b.png)

![](/media/1f92b191b4cdafeda75e6dbf4816f78b.png)

    #Import time and my74HC595 modules.
    from my74HC595 import Chip74HC595
    import time
    
    #Create a Chip74HC595 object and configure pins
    chip = Chip74HC595(14, 12, 13)
    # ESP32-14: 74HC595-DS(14)
    # ESP32-12: 74HC595-STCP(12)
    # ESP32-13: 74HC595-SHCP(11)
    
    #The first for loop makes LED Bar display separately from left to right
    #while the second for loop make it display separately from right to left.
    while True:
        x = 0x01
        for count in range(8):
            chip.shiftOut(1, x)
            x = x<<1;
            time.sleep_ms(300)
        x = 0x01
        for count in range(8):
            chip.shiftOut(0, x)
            x = x<<1
            time.sleep_ms(300)

6.  **Project result：**
    
Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/6129bf04efb1ce0373dbece47e630f00.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the 8 LEDs start flashing in flowing water
mode. Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”to exit the program.

![](/media/6f36d65ef0792431ed45b9c2ee0fc9ae.png)
