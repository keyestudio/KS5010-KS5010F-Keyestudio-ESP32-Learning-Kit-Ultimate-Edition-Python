# Project 32：RFID

1. Introduction： 

Nowadays, many residential districts use this function to open the
door by swiping the card, which is very convenient. In this Project,
we will learn how to use RFID(radio frequency identification)
wireless communication technology and read and write the key chain
card (white card) and control the steering gear rotation by
RFID-MFRC522 module.

2. Components：

|                                    |                        |                              |
| ---------------------------------- | ---------------------- | ---------------------------- |
| ![](/media/f12bee27e26177f00aa048f24499fc16.png) |
| ESP32\*1                           | Breadboard\*1          | RFID-RC522 Module\*1         |
| ![](/media/284218a1b5f1d347b1fd3c3119a34695.jpeg)  |
| M-F Dupont Wires                   | Servo\*1               | White Card\*1                |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)       |
| Key Chain\*1                       | Jumper wires           | USB Cable\*1                 |

Component knowledge：

**RFID：**RFID (Radio Frequency Identification) is a wireless
communication technology. A complete RFID system is generally composed
of the responder and reader. Generally, we use tags as responders, and
each tag has a unique code, which is attached to the object to identify
the target object. The reader is a device for reading (or writing) tag
information.

Products derived from RFID technology can be divided into three
categories: passive RFID products, active RFID products and semi active
RFID products. And Passive RFID products are the earliest, the most
mature and most widely used products in the market among others. It can
be seen everywhere in our daily life such as, the bus card, dining card,
bank card, hotel access cards, etc., and all of these belong to
close-range contact recognition. The main operating frequency of Passive
RFID products are: 125KHZ (low frequency), 13.56MHZ (high frequency),
433MHZ (ultrahigh frequency) and 915MHZ (ultrahigh frequency). Active
and semi active RFID products work at higher frequencies.

The RFID module we use is a passive RFID product with the operating
frequency of 13.56MHz.

**RFID-RC522 Module：**The MFRC522 is a highly integrated reader/writer
IC for contactless communication at 13.56MHz. The MFRC522's internal
transmitter is able to drive a reader/writer antenna designed to
communicate with ISO/IEC 14443 A/MIFARE cards and transponders without
additional active circuitry. The receiver module provides a robust and
efficient implementation for demodulating and decoding signals from
ISO/IEC 14443 A/MIFARE compatible cards and transponders. The digital
module manages the complete ISO/IEC 14443A framing and error detection
(parity and CRC) functionality.

This RFID Module uses MFRC522 as the control chip and adopts I2C
(Inter-Integrated Circuit) interface.

![](/media/5a19d0dd224c2cdc78871f11e8951045.png)

**Specifications:**

Operating voltage: DC 3.3V-5V

Operating current: 13—100mA/DC 5V

Idling current: 10-13mA/DC 5V

Sleep current: \<80uA

Peak current: \<100mA

Operating frequency: 13.56MHz

Maximum power: 0.5W

Supported card types: mifare1 S50, mifare1 S70, mifare UltraLight,
mifare Pro, mifare Desfire.

Environmental operating temperature: -20 to 80 degrees Celsius.

Environment storage temperature: -40 to 85 degrees Celsius.

Relative Humidity: 5% to 95%.

Data transfer rate: The maximum is 10Mbit/s.

4. RFID Read UID：

We will read the UNIQUE ID number (UID) of the RFID card and
identify the type of the RFID card, and display the relevant
information through the serial port. The wiring diagram is shown
below：

![](/media/1cdb3ffd7f392f29451aeed5c3257133.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
32：RFID”. Select“mfrc522\_config.py”,
“mfrc522\_i2c.py”and“soft\_iic.py”，right-click your mouse to
select“Upload to /”，wait for“mfrc522\_config.py”,
“mfrc522\_i2c.py”and“soft\_iic.py”to be uploaded to ESP32，and
double left-click“Project\_32.1\_RFID\_Read\_UID.py”.

![](/media/916442a2cb48ce3f1947cf054a748c06.png)

![](/media/a45492ec1d13bd480e86dc4cdc00aa0a.png)

![](/media/698154c5e3fb851ebe5d985b911ad0fa.png)

![](/media/0818507260684eab418555d922a92bb4.png)

    import machine
    import time
    from mfrc522_i2c import mfrc522
    
    #i2c config
    addr = 0x28
    scl = 22
    sda = 21
        
    rc522 = mfrc522(scl, sda, addr)
    rc522.PCD_Init()
    rc522.ShowReaderDetails()            # Show details of PCD - MFRC522 Card Reader details
    
    while True:
        if rc522.PICC_IsNewCardPresent():
            #print("Is new card present!")
            if rc522.PICC_ReadCardSerial() == True:
                print("Card UID:")
                print(rc522.uid.uidByte[0 : rc522.uid.size])
        #time.sleep(1)

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”.

![](/media/6027e4ff0c3b320eaf1d3ef5a466c915.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that place the door card and key chain close to
the module sensor area respectively, the "Shell" window of Thonny IDE
will display the card number and key chain value respectively, as shown
below. Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart
backend”to exit the program.

![](/media/44ff1db0c1d1964fa7bd386d96bcb13a.png)

![](/media/091b3f4fdd9b823b64487aec5d5834f8.png)

**Note:** the door card value and key chain value may be different for
different RRFID -RC522 door cards and key chains.

5. Wiring diagram of the RFID MFRC522：

Now we use the RFID -RC522 module, white card/key chain and Servo to
simulate an intelligent access control system. When the white
card/key chain close to the RFID -RC522 module induction area, the
servo rotates. Wiring according to the figure below：

![](/media/3ae6c0f1098d2aee34c51e7a96c25571.png)

6. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
32：RFID”. Select“mfrc522\_config.py”,
“mfrc522\_i2c.py”and“soft\_iic.py”，right-click your mouse to
select “Upload to /”，wait for “mfrc522\_config.py”,
“mfrc522\_i2c.py”and“soft\_iic.py”to be uploaded to ESP32，and
double left-click “Project\_32.2\_RFID\_Control\_Servo.py”.

![](/media/916442a2cb48ce3f1947cf054a748c06.png)

![](/media/a45492ec1d13bd480e86dc4cdc00aa0a.png)

![](/media/698154c5e3fb851ebe5d985b911ad0fa.png)

![](/media/816ff381b301d5a572ea706e9a061dd3.png)

    from machine import Pin, PWM
    import time
    from mfrc522_i2c import mfrc522
    
    #Define GPIO15’s output frequency as 50Hz and assign them to PWM.
    servoPin = Pin(15)
    pwm = PWM(servoPin, freq=50)
    
    #i2c config
    addr = 0x28
    scl = 22
    sda = 21
        
    rc522 = mfrc522(scl, sda, addr)
    rc522.PCD_Init()
    rc522.ShowReaderDetails()            # Show details of PCD - MFRC522 Card Reader details
    
    uid1 = [147, 173, 247, 32]
    uid2 = [57, 182, 70, 194]
    
    pwm = PWM(servoPin, freq=50)
    pwm.duty(128)
    time.sleep(1)
    
    while True:
        if rc522.PICC_IsNewCardPresent():
            #print("Is new card present!")
            if rc522.PICC_ReadCardSerial() == True:
                print("Card UID:", end=' ')
                print(rc522.uid.uidByte[0 : rc522.uid.size])
                if rc522.uid.uidByte[0 : rc522.uid.size] == uid1 or rc522.uid.uidByte[0 : rc522.uid.size] == uid2:
                    pwm = PWM(servoPin, freq=50)
                    pwm.duty(25)
                else :
                    pwm = PWM(servoPin, freq=50)
                    pwm.duty(128)
                time.sleep(500)

**Note: Different RFID-RC522 modules, ID cards and** key chains **may
different uid1 values and uid2 values.** The UID1 and UID2 values of the
white card and key chain read by your RRFID RC522 module can be replaced
by the corresponding values in the program code. If not,
click![](/media/da852227207616ccd9aff28f19e02690.png) **“Run current script” to r**un the code
may cause your own white card and key chain to fail to control the
servo.  

For example: You can replace the UID1 and UID2 values in the program
code![](/media/54b4d282380bd68468de99bbda6bd3ad.png)with your own white card and key chain
values.

**7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/845513c686a6674c6b13a7d69ecde448.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that when using the white card or a key card
swiping, the "Shell" window of Thonny IDE  displays the card number
value respectively, and at the same time, the servo rotates to the
corresponding angle to simulate opening the door. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” to exit the program.

![](/media/110c556e1106adf2304dee0725a98225.png)
