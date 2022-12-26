# Project 24：Night Lamp

1. Introduction：

Sensors or components are ubiquitous in our daily life. For example,
some public street lamps will automatically turn on at night and turn
off during the day. Why? In fact, this make use of a photosensitive
element that senses the intensity of external ambient light. When the
outdoor brightness decreases at night, the street lights will turn on
automatically; In the daytime, the street lights will automatically turn
off. the principle of which is very simple, In this Project, we use
ESP32 to control a LED to achieve the effect of the street light.

2. Components：

|                                    |                            |                             |                            |  |
| ---------------------------------- | -------------------------- | --------------------------- | -------------------------- |  |
| ![](/media/b395b1cd2678f87b3a34dec15659efbc.png) |  |
| ESP32\*1                           | Breadboard\*1              | Red LED\*1                  | 10KΩResistor\*1            |  |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)     |  |
| Photoresistor\*1                   | 220ΩResistor\*1            | Jumper Wires                | USB Cable\*1               |  |

3. Component knowledge：

![](/media/9e553e75b6f976f33438171eb2f2e775.png)

**Photoresistor :** It is a kind of photosensitive resistance, its
principle is that the photoresistor surface receives brightness (light)
to reduce the resistance, the resistance value will change with the
detected intensity of the ambient light . With this characteristic, we
can use the photosensitive resistance to detect the light intensity.
Photosensitive resistance and its electronic symbol are as follows：

![](/media/7d575da675a2f6cb511d28b801e2abaa.png)

The following circuit is used to detect changes in resistance values of
photoresistors：

![](/media/5a7f7e641eb78007760a94151c1d80a5.png)

In the circuit above, when the resistance of the photoresistor changes
due to the change of light intensity, the voltage between the
photoresistor and resistance R2 will also change.  Thus, the intensity
of light can be obtained by measuring this voltage.

4. Read the ADC value, DAC value and voltage value of the photoresistor：

We first use a simple code to read the ADC value, DAC value and voltage
value of the photoresistor and print them out. Please refer to the
following wiring diagram：

![](/media/b762098c798beb08e4d433137c317dc7.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
24：Night Lamp”，and then double left-click
“Project\_24.1\_Read\_Photosensitive\_Analog\_Value.py”.

![](/media/3da60098b23c3a7064ea660d3b028040.png)

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

![](/media/04f1cc092ddc2d54184978d85c3736a0.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the "Shell" window of Thonny IDE will print
the ADC value、DAC value and voltage value of the photoresistor. When the
light intensity around the photoresistor is gradually reduced, the ADC
value、DAC value and voltage value will gradually increase. On the
contrary, the ADC value、DAC value and voltage value decreases gradually.
Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to
exit the program.

![](/media/0e12e11c6998f995b2d57a4197a487f9.png)

![](/media/3b141ec51733d34caff4f0b2afc653a4.png)

5. Wiring diagram of the light-controlled lamp：

We made a small dimming lamp in the front, now we will make a light
controlled lamp. The principle is the same, that is, the ESP32 takes the
ADC value of the sensor, and then adjusts the brightness of the LED.

![](/media/77a0c534501f51e7fe7aa221e4db71d9.png)

6. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
24：Night Lamp”，and then double left-click
“Project\_24.2\_Night\_Lamp.py”.

![](/media/bbc7239d12d6561b17c2efbd427b3d54.png)

    from machine import Pin,PWM,ADC
    import time
    
    pwm =PWM(Pin(15,Pin.OUT),1000)
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_10BIT)
    
    try:
        while True:
            adcValue=adc.read()
            pwm.duty(adcValue)
            print(adc.read())
            time.sleep_ms(100)
    except:
        pwm.deinit()


7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/31f767ad280c34530e0abc6e845dd872.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that when the intensity of light around the
photoresistor is reduced, the LED will be bright, on the contraty, the
LED will be dim. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/15d9f8fca187dfe480cb8d11ea9a3816.png)
