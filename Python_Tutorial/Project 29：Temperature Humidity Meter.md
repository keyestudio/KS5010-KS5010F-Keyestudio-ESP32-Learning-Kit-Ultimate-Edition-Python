# Project 29：Temperature Humidity Meter 

1. Introduction：

In winter, the humidity in the air is very low, that is, the air is very
dry, Coupled with cold, the skin of the human body is easy to be too dry
and cracked, so you need to use a humidifier to increase the humidity of
the air at home, but how do you know that the air is too dry?Then you
need equipment to detect air humidity. In this Project, we will how to
use the temperature and humidity sensor. We use the sensor to make a
thermohygrometer, and also combined with a LCD 128X32 DOT to display the
temperature and humidity values.

2. Components：

|                                    |                             |                                    |
| ---------------------------------- | --------------------------- | ---------------------------------- |
| ![](/media/34bafe8113e2db36c8f0c8492b835474.png)     |
| ESP32\*1                           | Breadboard\*1               | Temperature and Humidity Sensor\*1 |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)             |
| LCD 128X32 DOT\*1                  | M-F Dupont Wires            | USB Cable\*1                       |

3. Component knowledge：

![](/media/34bafe8113e2db36c8f0c8492b835474.png)

**Temperature and humidity sensor:** It is a temperature and humidity
composite sensor with calibrated digital signal output, its precision
humidity is±5%RH, temperature is±2℃, range humidity is 20 to 90%RH, and
temperature is 0 to 50℃. The temperature and humidity sensor applies
dedicated digital module acquisition technology and temperature and
humidity sensing technology to ensure extremely high reliability and
excellent long-term stability of the product. The temperature and
humidity sensor includes a resistive-type humidity measurement and an
NTC temperature measurement component, which is very suitable for
temperature and humidity measurement applications where accuracy and
real-time performance are not required.

The operating voltage is in the range of 3.3V to 5.5V.

The temperature and humidity sensor has three pins, which are VCC、GNDand
S. S is the pin for data output, using serial communication.

**Single bus format definition of Temperature and Humidity Sensor：**

|                 |                                                                                                                                                                                                                                                      |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Description** | **Definition**                                                                                                                                                                                                                                       |
| Start signal    | Microprocessor pulls data bus (SDA) down at least 18ms for a period of time(Maximum is 30ms), notifying the sensor to prepare data.                                                                                                                  |
| Response signal | The sensor pulls the data bus (SDA) low for 83µs, and then pulls up for 87µs to respond to the host's start signal.                                                                                                                                  |
| Humidity        | The high humidity is an integer part of the humidity data, and the low humidity is a fractional part of the humidity data.                                                                                                                           |
| Temperature     | The high temperature is the integer part of the temperature data, the low temperature is the fractional part of the temperature data. And the low temperature Bit8 is 1, indicating a negative temperature, otherwise, it is a positive temperature. |
| Parity bit      | Parity bit=Humidity high bit+ Humidity low bit+temperature high bit+temperature low bit                                                                                                                                                              |

**Data sequence diagram** **of Temperature and Humidity Sensor：**

When MCU sends a start signal, the Temperature and Humidity Sensor
changes from the low-power-consumption mode to the high-speed mode,
waiting for MCU completing the start signal. Once it is completed, the
Temperature and Humidity Sensor sends a response signal of 40-bit data
and triggers a signal acquisition. The signal is sent as shown in the
figure:![](/media/933ac5e5a5e921d4b16c7c48091ba75a.png)

Combined with the code, you can understand better.

The XHT11 temperature and humidity sensor can easily add temperature and
humidity data to your DIY electronic projects. It is perfect for remote
weather stations, home environmental control systems, and farm or garden
monitoring systems.

**Specification:**

Working voltage: +5V

Temperature range: 0°C to 50°C, error of ± 2°C

Humidity range: 20% to 90% RH,± 5% RH error

Digital interface

**Schematic diagram of** **Temperature and Humidity Sensor:**

![](/media/53fa034cbbcec22579b2bdf8252c90cd.emf)

4. Read temperature and humidity value：

![](/media/5d6dd3f19b4323d212bb95e3e4d43743.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
29：Temperature Humidity Meter”, and then double left-click
“Project\_29.1\_Detect\_Temperature\_Humidity.py”.

![](/media/90be9f4eb3ce1fae8299a3dbbdd3f408.png)

    # Import machine, time and dht modules. 
    import machine
    import time
    import dht
    
    #Associate DHT11 with Pin(13).
    DHT = dht.DHT11(machine.Pin(13))
    
    # Obtain temperature and humidity data once per second and print them out. 
    while True:
        DHT.measure() # Start DHT11 to measure data once.
       # Call the built-in function of DHT to obtain temperature
       # and humidity data and print them in “Shell”.
        print('temperature:',DHT.temperature(),'℃','humidity:',DHT.humidity(),'%')
        time.sleep_ms(1000)

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/941cb120d0f127710bf047301de8ba3a.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, if the temperature and
humidity sensor is incorrectly connected, the following information is
displayed in the “Shell”window. Please make sure your circuit is
properly connected. Click![](/media/da852227207616ccd9aff28f19e02690.png)again, the code starts
to be executed and you'll see that the "Shell" window of Thonny IDE will
print the temperature and humidity datas in the current surroundings, as
shown in the following figure. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/0f06c1e7a47dc8ad49e9accccc69924b.png)

![](/media/87fe0032fe9236d8e94484445b720605.png)

![](/media/3561864f71474f8e8c7206c07c8d054e.png)

5. Wiring diagram of the thermohygrometer：

Now we start to print the values of the temperature and humidity sensor
with LCD\_128X32\_DOT. We will see the corresponding values on the
screen of LCD\_128X32\_DOT. Let's get started with this project. Please
connect cables according to the following wiring diagram：

![](/media/6c82bb28bd1fcd7a1f72108e8a4a70b6.png)

6. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
29：Temperature Humidity Meter”.
Select“lcd128\_32.py”and“lcd128\_32\_fonts.py”，right-click your
mouse to select“Upload to /”，wait
for“lcd128\_32.py”and“lcd128\_32\_fonts.py”to be uploaded to
ESP32，and double left-click
“Project\_29.2\_Temperature\_Humidity\_Meter.py”.

![](/media/e2c0a6bba216d886d1d00dad87cf763c.png)

![](/media/60698b0bc0945674fdaaff76d09967ae.png)

![](/media/818896cf745064f9d5346c43b1282554.png)

    from machine import Pin
    import machine
    import dht
    import time
    import lcd128_32_fonts
    from lcd128_32 import lcd128_32
    
    temp = 0
    humi = 0
    
    #Associate DHT11 with Pin(13).
    DHT = dht.DHT11(Pin(13))
    
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
            DHT.measure()
            temp = int(DHT.temperature())
            humi = int(DHT.humidity())
            if use_i2c:
                scan_for_devices()
                lcd = lcd128_32(data_pin, clock_pin, bus, i2c_addr)         
            lcd.Clear()
            lcd.Cursor(0, 0)
            lcd.Display("temper:")
            lcd.Cursor(0, 8)
            lcd.Display(str(temp))
            lcd.Cursor(0, 11)
            lcd.Display("C")
            lcd.Cursor(2, 0)
            lcd.Display("Humid:")
            lcd.Cursor(2, 7)
            lcd.Display(str(humi))
            lcd.Cursor(2, 10)
            lcd.Display("%")
            time.sleep(0.1)
    except:
        pass

7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/09cb361dc3793f243a6a428398bfdc90.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the LCD 128X32 DOT will display temperature
and humidity value in the current environment. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” to exit the program.

![](/media/c09f7ded241ef13687c0c0d56dc5d8c8.png)
