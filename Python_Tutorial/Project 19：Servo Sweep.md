# Project 19：Servo Sweep

1. Introduction：

Servo is an electric motor that can rotate very precisely. At present,
it has been widely used in toy cars，remote control
helicopters，airplanes，robots, etc. In this project, we will use
ESP32 to control the rotation of the servo.

2. Components：

|                                    |                        |                        |
| ---------------------------------- | ---------------------- | ---------------------- |
| ![](/media/e380dd26e4825be9a768973802a55fe6.png) |                        |
| ESP32\*1                           | Breadboard\*1          |                        |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png) |
| Servo\*1                           | Jumper Wires           | USB Cable\*1           |

3. Component knowledge：

**Servo：**

![](/media/99830768916233a9c5900ac399006c17.png)

The servo is a kind of position servo driver, which is mainly composed
of housing、circuit board、copless motor、gear and position detector. Its
working principle is that the receiver or microcontroller sends a signal
to the servo which has an internal reference circuit that generates a
reference signal with a period of 20ms and a width of 1.5ms, and
compares the DC bias voltage with the voltage of the potentiometer to
output voltage difference.The IC on the circuit board determines the
direction of rotation, and then drives the coreless motor to start
rotation and transmits the power to the swing arm through the reduction
gear, while the position detector sends back a signal to determine
whether it has reached the positioning. It is suitable for those control
systems that require constant change of angle and can be maintained.
When the motor rotates at a certain speed, the potentiometer is driven
by the cascade reduction gear to rotate so that the voltage difference
is 0 and the motor stops rotating. The angle range of general servo
rotation is 0 to 180 degrees.

The pulse period for controlling the servo is 20ms, the pulse width is
0.5ms to 2.5ms, and the corresponding position is -90 degrees to +90
degrees. The following is an example of a 180 degree servo：

![](/media/708316fde05c62113a3024e0efb0c237.jpeg)

Servo motors have many specifications, but they all have three
connecting wires, which are brown, red, and orange (different brands may
have different colors). The brown is GND, the red is the positive power
supply, and the orange is the signal line.

![](/media/3f5bc31305e64108bed3b3619d602891.jpeg)

4. Wiring Diagram：

When supplying the servo, please note that the power supply voltage
should be 3.3V-5V. Make sure there are no errors when connecting the
servo to the power supply.

![](/media/39621cc861e5f7c189a047b7f0bbd0be.png)

5. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
19：Servo Sweep”. Select“myservo.py”，right-click your mouse to
select“Upload to /”，wait for“myservo.py”to be uploaded to ESP32，and
then double left-click“Project\_19\_Servo\_Sweep.py”.

![](/media/61723626d98b37ffdaa0d9faffc374c9.png)

![](/media/7faf94bca6fd3a17bb276b31f7531a34.png)

    from myservo import myServo #Import myservo module.
    import time
    
    #Initialize pins of the servo and set the starting point of the servo to 0 degree.
    servo=myServo(15)
    servo.myServoWriteAngle(0)
    time.sleep_ms(1000)
    
    try:
        while True:
    #Use two for loops. The first one controls the servo to rotate from 0 degree to 180 degrees
    #while the other controls it to rotate back from 180 degrees to 0 degree.
            for i in range(0,180,1):
                servo.myServoWriteAngle(i) #Control the servo to rotate to a specified angle within the range of 0-180 degrees.
                time.sleep_ms(15)
            for i in range(180,0,-1):
                servo.myServoWriteAngle(i)
                time.sleep_ms(15)        
    except:
        servo.deinit()

6. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend” .

![](/media/01a44d90da6e1717fa34e87db3848db3.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that the Servo will rotate from 0 degrees to 180
degrees and then reverse the direction to make it rotate from 180
degrees to 0 degrees and repeat these actions in an endless loop.
Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to
exit the program.

![](/media/22a9496d01eadd96c9184375011a5c61.png)

![](/media/c5250405a4290ecb2d758ff1097310c7.png)
