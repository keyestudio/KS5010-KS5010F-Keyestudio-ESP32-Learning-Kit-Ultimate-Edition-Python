# Project 33：Keypad Door

1. Introduction：

Commonly used digital button sensor, one button uses an IO port.
However, it will occupy too many IO ports when we need a lot of
buttons. In order to save the use of IO ports, the multiple buttons
are made into a matrix type, through the control of the line and row
to achieve less IO port control of multiple buttons. In this
project, we will learn ESP32 and thin film 4\*4 matrix keyboard
control a servo and a buzzer.

2. Components：

|                                    |                        |                        |                                                  |
| ---------------------------------- | ---------------------- | ---------------------- | ------------------------------------------------ |
| ![](/media/4b4f653a76a82a3b413855493cc58fba.png) |
| ESP32\*1                           | Breadboard\*1          | Servo\*1               | Active Buzzer\*1                                 |
| ![](/media/098a2730d0b0a2a4b2079e0fc87fd38b.png)                           |
| 4\*4 Membrane Matrix Keyboard\*1   | Jumper Wires           | USB Cable\*1           | 1kΩResistor\*1                                   |
| ![](/media/9197d4aff9356c585b7ef68e33a6881d.png)            |                        |                        |                                                  |
| NPN transistor(S8050)\*1           |                        |                        |                                                  |

3. Component knowledge：

**4\*4 Matrix keyboard：**A Keypad Matrix is a device that integrates a
number of keys in one package. As is shown below, a 4x4 Keypad Matrix
integrates 16 keys:

![](/media/fcd187eb009098d691927511606c991b.jpeg)

Similar to the integration of an LED Matrix, the 4x4 Keypad Matrix has
each row of keys connected with one pin and this is the same for the
columns. Such efficient connections reduce the number of processor ports
required. The internal circuit of the Keypad Matrix is shown below.

![](/media/5ebdacba906622079e0ef41dc1ea3fdf.png)

The method of usage is similar to the Matrix LED, by using a row or
column scanning method to detect the state of each key’s position by
column and row. Take column scanning method as an example, send low
level to the first 4 column (Pin4), detect level state of row 1, 2, 3, 4
to judge whether the key A, B, C, D are pressed. Then send low level to
column3, 2, 1 in turn to detect whether other keys are pressed. By this
means, you can get the state of all of the keys.

4. Read the key value of the 4\*4 matrix keyboard：

We start with a simple code to read the values of the 4\*4 matrix
keyboard and print them in the serial monitor. Its wiring diagram is
shown below：

![](/media/8bfa0e1b1a0f53598f51341d51bc7601.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
33：Keypad Door”. Select“keypad.py”，right-click your mouse to
select“Upload to /”，wait for“keypad.py” to be uploaded to ESP32，and
double left-click“Project\_33.1\_4x4\_Matrix\_Keypad\_Display.py”.

![](/media/461e72b6f3431cb4efc0972e97ca79ee.png)

![](/media/cc7e58a56e83cc25c1ee09d9cd49ecc6.png)

    # Import keypad module.
    from keypad import KeyPad
    import time
    # Associate the keypad module to ESP32 pins. 
    keyPad = KeyPad(22, 21, 19, 18, 17, 16, 4, 0)
    #Call function keyPan.scan() to obtain the value of the pressed key. Once it is obtained, print it out. 
    def key():
        keyvalue = keyPad.scan()
        if keyvalue != None:
            print(keyvalue, end="\t")
            time.sleep_ms(300)
            return keyvalue
                
    while True:
        key()


Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”.

![](/media/6ee2f497a98d196c9489e2bff23198dd.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that press the keyboard and the "Shell" window
of Thonny IDE prints the corresponding key value, as shown below.
Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to
exit the program.

![](/media/3ed02181a152283b15b9e2c612ef52ea.png)

![](/media/2f82f861d68daaaad8085b6a1bcc2e8d.png)

5. Wiring diagram of the Keypad Door：

In the last experiment, we have known the key values of the 4\*4 matrix
keyboard. Next, we use it as the keyboard to control a servo and a
buzzer.

![](/media/862e840117a46c1174522a734e28e2f0.png)

6. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project 33：
Keypad Door”. Select“keypad.py”and “myservo.py”，right-click your mouse
to select“Upload to /”，wait for“keypad.py”and“myservo.py”to be uploaded
to ESP32，and double left-click “Project\_33.2\_Keypad\_Door.py”.

![](/media/461e72b6f3431cb4efc0972e97ca79ee.png)

![](/media/7cc5b83570afc6e43469747002ed6aa5.png)

![](/media/ba149f6670bb32c838ab0e436fa05af7.png)

    from myservo import myServo #Import myservo module.
    from keypad import KeyPad
    from machine import Pin
    import time
    
    keyPad = KeyPad(22, 21, 19, 18, 17, 16, 4, 0)
    servo=myServo(15)
    servo.myServoWriteAngle(0)
    time.sleep_ms(1000)
    activeBuzzer = Pin(2, Pin.OUT)
    
    # Define an array and set the password. 
    passWord = "1234"
    keyIn = ""
    def key():
        keyvalue = keyPad.scan()
        if keyvalue != None:
            print('Your input:', keyvalue)
            time.sleep_ms(200)
            return keyvalue
    
    while True:
     # Each time a key is pressed, the buzzer will short beep once,
     # and the key value of the key will be stored in the keyIn array. 
        keydata = key()
        if keydata != None:
            activeBuzzer.value(1)
            time.sleep_ms(100)
            activeBuzzer.value(0)
            keyIn += keydata 
    # When 4 keys are pressed, it will judge whether the password is correct.
    # If it is correct, the servo will rotate 90 degrees, and then turn back after 1 second.
    # If the password is wrong, the buzzer will long beep once and the keyInNum value will be cleared.        
        if len(keyIn) == 4:
            if keyIn == passWord:
                print("passWord right!")
                servo.myServoWriteAngle(90)
                time.sleep_ms(1000)
                servo.myServoWriteAngle(0)
            else:
                print("passWord error!")
                activeBuzzer.value(1)
                time.sleep_ms(1000)
                activeBuzzer.value(0)
            keyIn = ""

7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”.

![](/media/930debbfbad2a57398b43013a04f39e6.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that press the keypad to input password with 4
characters. If the input is correct(Correct password :1234), the servo
will move to a certain degree, and then return to the original position.
If the input is wrong, an input error alarm will be generated.

Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to
exit the program.

![](/media/84a92736ba4eb3a965bff7ecfb72b57f.png)

![](/media/d45bd766b2b2630219f8bef283a07417.png)
