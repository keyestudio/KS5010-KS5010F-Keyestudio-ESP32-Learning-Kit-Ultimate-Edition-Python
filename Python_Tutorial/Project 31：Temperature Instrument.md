# Project 31：Temperature Instrument

1. Introduction：

Thermistor is a kind of resistor whose resistance depends on
temperature changes, which is widely used in gardening, home alarm
system and other devices. Therefore, we can use the feature to make
a temperature instrument.

2. Components：

|                                    |                         |                        |                            |
| ---------------------------------- | ----------------------- | ---------------------- | -------------------------- |
| ![](/media/b395b1cd2678f87b3a34dec15659efbc.png) |
| ESP32\*1                           | Breadboard\*1           | Thermistor\*1          | 10KΩResistor\*1            |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)     |
| M-F Dupont Wires                   | LCD 128X32 DOT\*1       | Jumper Wires           | USB Cable\*1               |

3. Component knowledge：

**Thermistor:** A Thermistor is a temperature sensitive resistor. When
it senses a change in temperature, the resistance of the Thermistor will
change. We can take advantage of this characteristic by using a
Thermistor to detect temperature intensity. A Thermistor and its
electronic symbol are shown below:

![](/media/809b8634747fb295021f12e3b92b7894.png)

The relationship between resistance value and temperature of a
thermistor is：

**Where:**

**Rt** is the thermistor resistance under T2 temperature;

**R** is the nominal resistance of thermistor under T1 temperature;

**EXP\[n\]** is nth power of e;

**B** is for thermal index;

**T1, T2** is Kelvin temperature (absolute temperature). Kelvin
temperature=273.15 + Celsius temperature.

For the parameters of the Thermistor, we use: B=3950, R=10k, T1=25.

The circuit connection method of the Thermistor is similar to
photoresistor, as the following：

![](/media/b0f80e9bd350a8b7390a73756ac1ac8c.jpeg)

We can use the value measured by the ADC converter to obtain the
resistance value of Thermistor, and then we can use the formula to
obtain the temperature value.

Therefore, the temperature formula can be derived as:：

4. Read the value of the Thermistor：

First we will learn the thermistor to read the current ADC value,
voltage value and temperature value and print them out. Please
connect the wires according to the wiring diagram below：

![](/media/806fd81bf8a761b4ae1a638489c426ce.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
31：Temperature Instrument”, and then double left-click
“Project\_31.1\_Read\_the\_thermistor\_analog\_value.py”.

![](/media/475ecb7774bdbd2c778f57995014e55c.png)

    from machine import Pin, ADC
    import time
    import math
    
    #Set ADC
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_12BIT)
    
    try:
        while True:
            adcValue = adc.read()
            voltage = adcValue / 4095 * 3.3
            Rt = 10 * voltage / (3.3-voltage)
            tempK = (1 / (1 / (273.15+25) + (math.log(Rt/10)) / 3950))
            tempC = (tempK - 273.15)
            print("ADC value:",adcValue,"  Voltage:",voltage,"V","  Temperature: ",tempC,"C");
            time.sleep(1)
    except:
        pass

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”.

![](/media/eb091a4f3318bd57b1b936708d9a2501.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the "Shell" window of Thonny IDE will
continuously display the thermistor's current ADC value、voltage value
and temperature value. Try pinching the thermistor with your index
finger and thumb (don't touch wires) for a while, and you will see the
temperature increase. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/e4670e9a95847f531dbcf6707dcad5ef.png)

![](/media/77f18a9e099306cd7111d6b2df2b5eb6.png)

5. Wiring diagram of the temperature instrument：

![](/media/5a437bfdcad012211e15cab54e35dad7.png)

6. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
31：Temperature Instrument”. Select“lcd128\_32.py”and
“lcd128\_32\_fonts.py”，right-click your mouse to select“Upload to
/”，wait for“lcd128\_32.py”and“lcd128\_32\_fonts.py”to be uploaded to
ESP32，and double left-click“Project\_31.2\_Temperature\_Instrument.py”.

![](/media/0e356b1ae181188b13379fa49b4f1cea.png)

![](/media/44607b3cc5159abef2a33da1a4e89e0c.png)

![](/media/14ab39df40a24015811265442102f446.png)

    from machine import Pin, ADC, I2C
    import machine
    import time
    import math
    import lcd128_32_fonts
    from lcd128_32 import lcd128_32
    
    #Set ADC
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_12BIT)
    
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
            
    try:
        while True:
            adcValue = adc.read()
            voltage = adcValue / 4095 * 3.3
            Rt = 10 * voltage / (3.3-voltage)
            tempK = (1 / (1 / (273.15+25) + (math.log(Rt/10)) / 3950))
            tempC = int(tempK - 273.15)        
            if use_i2c:
                scan_for_devices()
                lcd = lcd128_32(data_pin, clock_pin, bus, i2c_addr)  
            lcd.Clear()
            lcd.Cursor(0, 0)
            lcd.Display("Voltage:")
            lcd.Cursor(0, 8)
            lcd.Display(str(voltage))
            lcd.Cursor(0, 20)
            lcd.Display("V")
            lcd.Cursor(2, 0)
            lcd.Display("Temperature:")
            lcd.Cursor(2, 12)
            lcd.Display(str(tempC))
            lcd.Cursor(2, 15)
            lcd.Display("C")
            time.sleep(0.5)
    except:
        pass

7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/a65a4b4747eae37f299d7c8b0c3bd4d9.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the LCD 128X32 DOT displays the voltage
value of the thermistor and the temperature value in the current
environment. Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”to exit the program.

![](/media/c040915c339326f76155d6a3b2e1f695.png)
