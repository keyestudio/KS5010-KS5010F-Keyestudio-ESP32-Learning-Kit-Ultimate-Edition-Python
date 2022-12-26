# Project 23：Flame Alarm

1. Introduction：

Fire is a terrible disaster and fire alarm systems are very useful in
houses、commercial buildings and factories. In this project, we will use
ESP32 to control a flame sensor, a buzzer and a LED to simulate fire
alarm devices. This is a meaningful maker activity.

2. Components：

|                                    |                            |                             |                                                  |
| ---------------------------------- | -------------------------- | --------------------------- | ------------------------------------------------ |
| ![](/media/4b4f653a76a82a3b413855493cc58fba.png) |
| ESP32\*1                           | Breadboard\*1              | Red LED\*1                  | Active Buzzer\*1                                 |
| ![](/media/e9a8d050105397bb183512fb4ffdd2f6.png)                           |
| Flame Sensor\*1                    | 220ΩResistor\*1            | 10KΩResistor\*1             | Jumper Wires                                     |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)     |                                                  |
| NPN transistor(S8050)\*1           | 1kΩ Resistor\*1            | USB Cable\*1                |                                                  |

3. Component knowledge：

![](/media/a50ec3e38adf10643eafac8cb62bec8a.png)

The flame emits a certain amount IR light that is invisible to the human
eye, but our flame sensor can detect it and alert a microcontroller
(such as ESP32) that a fire has been detected. It has a specially
designed infrared receiver tube to detect the flame and then convert the
flame brightness into a fluctuating level signal. The short pin of the
receiving triode is negative pole and the other long pin is positive
pole. We should connect the short pin (negative) to 5V and the long pin
(positive) to the analog pin, a resistor and GND. As shown in the figure
below：

![](/media/87bd204db523c602c80745266c1ee452.png)

**Note:** Since vulnerable to radio frequency radiation and temperature
changes, the flame sensor should be kept away from heat sources like
radiators, heaters and air conditioners, as well as direct irradiation
of sunlight, headlights and incandescent light.

4. Read the ADC value, DAC value and voltage value of the flame sensor：

We first use a simple code to read the ADC value, DAC value and voltage
value of the flame sensor and print them out. Please refer to the wiring
diagram below：

![](/media/76ce57355da1df27e049bdc6e19f0650.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
23：Flame Alarm”，and then double left-click
“Project\_23.1\_Read\_Analog\_Value\_Of\_Flame\_Sensor.py”.

![](/media/b4ab4d56badbead366bed085d382f224.png)

    # Import Pin, ADC and DAC modules.
    from machine import ADC,Pin,DAC
    import time
    
    # Turn on and configure the ADC with the range of 0-3.3V 
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_12BIT)
    
    # Read ADC value once every 0.1seconds, convert ADC value to DAC value and output it,
    # and print these data to “Shell”. 
    try:
        while True:
            adcVal=adc.read()
            dacVal=adcVal//16
            voltage = adcVal / 4095.0 * 3.3
            print("ADC Val:",adcVal,"DACVal:",dacVal,"Voltage:",voltage,"V")
            time.sleep(0.1)
    except:
        pass

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/c2ec0600962bd87b24376fc0986183c4.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the "Shell" window of Thonny IDE will print
the ADC value、DAC value and voltage value of the flame sensor. When the
flame is close to the flame sensor, the ADC value, DAC value and voltage
value increase; Conversely, the ADC value, DAC value and voltage value
decrease. Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”to exit the program.

![](/media/8cfd1510ef6c947201dd14ff0f5ade21.png)

![](/media/65e6848785b8e09c731df4dd1f68a3a0.png)

5. Wiring diagram of the flame alarm：

Next, we will use a flame sensor, a buzzer, and a LED to make an
interesting project, that is flame alarm. When flame is detected, the
LED flashes and the buzzer alarms.

![](/media/e9fa0e50df23c1f2e58fdd319ad21b4c.png)

6. Project code：（Note：![](/media/40a3ea572836945268b22dfc0cce29c3.png) the threshold of 500
in the code can be reset itself as required）

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
23：Flame Alarm”, and then double left-click
“Project\_23.2\_Flame\_Alarm.py”.

![](/media/08b1420f2793b1c20200af63ce5111ba.png)

    from machine import ADC, Pin
    import time
    
    # Turn on and configure the ADC with the range of 0-3.3V 
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_12BIT)
    # create LED object from Pin 15,Set Pin 15 to output
    led = Pin(15, Pin.OUT) 
    # create buzzer object from Pin 4, Set Pin 4 to output
    buzzer = Pin(4, Pin.OUT)   
     
    # If the flame sensor detects a flame, the buzzer will beep
    # and the LED will blink when the analog value is greater than 500
    # Otherwise, the buzzer does not sound and the LED goes off 
    while True:
        adcVal=adc.read()
        if adcVal >500:
            buzzer.value(1)    # Set buzzer turn on
            led.value(1)    # Set led turn on
            time.sleep(0.5) # Sleep 0.5s
            buzzer.value(0) 
            led.value(0)    # Set led turn off
            time.sleep(0.5) # Sleep 0.5s
        else:
            buzzer.value(0)    # Set buzzer turn off
            led.value(0)    # Set led turn off


7.  **Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/16f7214c93439af62ac8d2a005b398ea.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that when the flame sensor detects the flame,
the LED flashes and the buzzer alarms. Otherwise, the LED does not
light, the buzzer does not sound.Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/a13d1483a5d9bca9258d760f3dbb4ac8.png)
