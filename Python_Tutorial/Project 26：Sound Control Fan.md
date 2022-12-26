# Project 26：Sound Control Fan

1. Introduction：

The sound sensor has a built-in capacitive electret microphone and power
amplifier which can be used to detect the sound intensity of the
environment. In this project, we use ESP32 to control the sound sensor
and the motor module to simulate a voice-controlled fan.

2. Components：

|                                                |                             |                                 |
| ---------------------------------------------- | --------------------------- | ------------------------------- |
| ![](/media/435be010afaa963d94ffe82d01020ff5.png)         |
| ESP32\*1                                       | Breadboard\*1               | Sound Sensor\*1                 |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)          |
| 130 Motor Module\*1                            | M-F Dupont Wires            | USB Cable\*1                    |
| ![](/media/a815c48437199c6ab79d74cd2d583de0.png)         |
| Keyestudio bread board special power module\*1 | Battery Holder\*1           | No.5 battery (self-provided)\*6 |
| ![](/media/009965e315276ecf1144c22c54a93fd9.png)                        |                             |                                 |
| Fan\*1                                         |                             |                                 |

3. Component knowledge：

![](/media/9271d5f7a7647d7a3c959e6c7b837b5b.png)

Sound sensor is usually used to detect the loudness of the sound in the
surrounding environment. Microcontrol board can collect its output
signal through the analog input interface.The S pin is an analog output,
which is the real-time output of the microphone voltage signal. The
sensor comes with a potentiometer so you can adjust the signal strength.
It also has two fixing holes so that the sensor can be installed on any
other equipment. You can use it to make some interactive works, such as
voice-operated switches.

4. Read the ADC value, DAC value and voltage value of the sound sensor：

We first use a simple code to read the ADC value, DAC value and voltage
value of the sound sensor and print them out. Please refer to the wiring
diagram below：

![](/media/87fb44c475d1f53aa5905cebfed55ea2.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
26：Sound Control Fan”, and then double left-click
“Project\_26.1\_Read\_Sound\_Sensor\_Analog\_Value.py”.

![](/media/7e36b481b74dcb94e2f7eae034f10e46.png)

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

![](/media/ecd790660a245d0a3dd979014763c638.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the "Shell" window of Thonny IDE will print
the ADC value，DAC value and voltage value of the sound sensor，When you
clap your hands to the sensor, the ADC value, DAC value and voltage
value will change significantly. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/cbadc7277e1970b3b0ac78cf54efb0cf.png)

![](/media/16c179e59bfbbb62544d74ce501f0aa2.png)

5. Wiring diagram of the intelligent fan：

Next, we officially entered the project. We used a sound sensor, a motor
module and a fan blade to simulate a voice-controlled fan. The wiring
diagram is as follows：

![](/media/5a08d512265e03c997bf81a9e2bfecbb.png)

(Note: Connect the wires and then install a small fan blade on the DC
motor. )

6. Project code：（Note：![](/media/c20911df19d11290cf099072fe250029.png)The threshold 600 in
the code can be reset itself as needed）

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
26：Sound Control Fan”，and then double left-click
“Project\_26.2\_Sound\_Control\_Fan.py”.

![](/media/1eb18932f71867f625af510747c7a45a.png)

    from machine import ADC, Pin
    import time
     
    # Turn on and configure the ADC with the range of 0-3.3V 
    adc=ADC(Pin(36))
    adc.atten(ADC.ATTN_11DB)
    adc.width(ADC.WIDTH_12BIT)
     
    # Pin initialization
    motor1a = Pin(15, Pin.OUT) # create motor1a object from Pin 15, Set Pin 15 to output
    motor1b = Pin(2, Pin.OUT) # create motor1b object from Pin 2, Set Pin 2 to output
    
    # If the Sound sensor detects Sounds, and the motor will rotate
    # when the analog value is greater than 600,Otherwise, the motor does not rotate.    
    while True:
        adcVal=adc.read()
        print(adcVal)
        time.sleep(0.5)
        if adcVal >600:
            motor1a.value(1) # Set motor1a high
            motor1b.value(0) # Set motor1b low
            time.sleep(5)   # delay time 
        else:
            motor1a.value(0)
            motor1b.value(0)

7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/f987f5ba18e896faec48b502d6e92493.png)

External power supply and power on. Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run
current script”, the code starts to be executed and you'll see that clap
your hands to the sound sensor, and when the sound intensity exceeds a
threshold, the small fan rotates;  conversely, the small fan doesn't
rotate. Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”to exit the program.

![](/media/d0d4432fea99db80f84a4b15291b612f.png)
