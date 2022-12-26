# Project 17： I2C 128×32 LCD

1. Introduction：

In everyday life, we can do all kinds of experiments with the display
module and also DIY a variety of small objects. For example, you can
make a temperature meter with a temperature sensor and display, or make
a distance meter with an ultrasonic module and display. In this project,
we will use the LCD\_128X32\_DOT module as the display and connect it to
the ESP32, which will be used to control the LCD\_128X32\_DOT display to
display various English words, common symbols and numbers.

2. Components：

|                                    |                             |                        |
| ---------------------------------- | --------------------------- | ---------------------- |
| ![](/media/e380dd26e4825be9a768973802a55fe6.png)      |                        |
| ESP32\*1                           | Breadboard\*1               |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| LCD\_128X32\_DOT\*1                | M-F Dupont Wires            | USB Cable\*1           |

3. Component knowledge：

![](/media/2c2645e94a00867ac23e8a022f0a631a.png)

**LCD\_128X32\_DOT:** It is an LCD module with 128\*32 pixels and its
driver chip is ST7567A. The module uses the IIC communication mode,
while the code contains a library of all alphabets and common symbols
that can be called directly. When using, we can also set it in the code
so that the English letters and symbols show different text sizes. To
make it easy to set up the pattern display, we also provide a mold
capture software that converts a specific pattern into control code and
then copies it directly into the test code for use.

**Schematic diagram of LCD\_128X32\_DOT：**

![](/media/5451aed32bc5b7b30fbd5613ad09a65b.png)

**Features:**

Pixel: 128\*32 character

Operating voltage(chip)：4.5V to 5.5V

Operating current：100mA (5.0V)

Optimal operating voltage(module):5.0V

4. Wiring Diagram：

![](/media/072d954dac310add077688398ad59af2.png)

5. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project 17：
I2C 128×32 LCD”. Select“lcd128\_32.py”and
“lcd128\_32\_fonts.py”，right-click your mouse to select“Upload to
/”，wait for“lcd128\_32.py”and“lcd128\_32\_fonts.py”to be uploaded to
ESP32，and then double left-click“Project\_17\_I2C\_128\_32\_LCD.py”.

![](/media/9324aa3246b032463d5462c0eb7ac848.png)

![](/media/dfc274fafadf864413e7d1b7f8c91dc4.png)

![](/media/e5135a82011f1291505aff96fc88b7ac.png)

    import machine
    import time
    import lcd128_32_fonts
    from lcd128_32 import lcd128_32
    
    #i2c config
    clock_pin = 22
    data_pin = 21
    bus = 0
    i2c_addr = 0x3f
    use_i2c = True
    
    def scan_for_devices():
        i2c = machine.I2C(bus,sda=machine.Pin(data_pin),scl=machine.Pin(clock_pin))
        devices = i2c.scan()
        if devices:
            for d in devices:
                print(hex(d))
        else:
            print('no i2c devices')
    
    
    if use_i2c:
        scan_for_devices()
        lcd = lcd128_32(data_pin, clock_pin, bus, i2c_addr)
    
    
    lcd.Clear()
    
    lcd.Cursor(0, 4)
    lcd.Display("KEYESTUDIO")
    lcd.Cursor(1, 0)
    lcd.Display("ABCDEFGHIJKLMNOPQR")
    lcd.Cursor(2, 0)
    lcd.Display("123456789+-*/<>=$@")
    lcd.Cursor(3, 0)
    lcd.Display("%^&(){}:;'|?,.~\\[]")
    """
    while True:
        scan_for_devices()
        time.sleep(0.5)
    """

6. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/a1273c3f5019666f8f2de2b18504e77c.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the 128X32LCD module display will
show“KEYESTUDIO”at the first line，“ABCDEFGHIJKLMNOPQR”will be
displayed at the second line，“123456789+-\*/\<\>=$@”will be shown at the
third line and“%^&(){}:;'|?,.\~\\\\\[\]”will be displayed at the fourth
line. Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”to exit the program.

![](/media/4834a36715ea72a01498a6077402a033.png)
