# Project 34：IR Control Sound and LED

1. Introduction：

An infrared(IR) remote control is a low-cost and easy-to-use wireless
communication technology. IR light is very similar to visible light,
except that its wavelength is slightly longer. This means that infrared
rays cannot be detected by the human eye, which is perfect for wireless
communication. For example, when you press a button on the TV remote
control, an infrared LED will switch on and off repeatedly at a
frequency of 38,000 times per second, transmitting information (such as
volume or channel control) to the infrared sensor on the TV.

We'll start by explaining how common infrared communication protocols
work. Then we will start the project with a remote control and an
infrared receiver component.

2. Components：

|                                    |                                                  |                            |                                 |
| ---------------------------------- | ------------------------------------------------ | -------------------------- | ------------------------------- |
| ![](/media/f1a86fc81ab4b043263ce7e01e14d470.png) |
| ESP32\*1                           | Breadboard\*1                                    | IR Receiver \*1            | RGB LED\*1                      |
| ![](/media/098a2730d0b0a2a4b2079e0fc87fd38b.png)          |
| IR Remote Controller\*1            | Active buzzer\*1                                 | 10KΩResistor\*1            | 220ΩResistor\*3                 |
| ![](/media/7dcbd02995be3c142b2f97df7f7c03ce.png)         |
| NPN transistor(S8050)\*1           | 1kΩResistor\*1                                   | Jumper Wires               | USB Cable\*1                    |

3. Component knowledge：

**Infrared Remote：**An infrared(IR) remote control is a device with a
certain number of buttons. Pressing down different buttons will make the
infrared emission tube, which is located in the front of the remote
control, send infrared ray with different command. Infrared remote
control technology is widely used in electronic products such as
TV、airconditioning, etc. Thus making it possible for you to switch TV
programs and adjust the temperature of the air conditioning when away
from them. The remote control we use is shown below:

The infrared remote controller adopts NEC code and the signal cycle is
110ms.

![](/media/3c9d76cb0d24d9861811ce2cb0bb6ae4.png)

**Infrared receiver：**receiver is a component which can receive the
infrared light, so we can use it to detect the signal emitted by the
infrared remote control.

The infrared receiver demodules the received infrared signal and
converts it back to binary, then passes the information to the
microcontroller.

**Infrared signal modulation process diagram：**

![](/media/3da1969e509f53706643c77d0534eb73.png)

**NEC Infrared communication protocol：**

**NEC Protocol:**

To my knowledge the protocol I describe here was developed by NEC (Now
Renesas). I've seen very similar protocol descriptions on the internet,
and there the protocol is called Japanese Format.  
I do admit that I don't know exactly who developed it. What I do know is
that it was used in my late VCR produced by Sanyo and was marketed under
the name of Fisher. NEC manufactured the remote control IC.  
This description was taken from my VCR's service manual. Those were the
days, when service manuals were filled with useful information\!

**Features:**

- > \* 8 bit address and 8 bit command length.

- > \* Extended mode available, doubling the address size.

- > \* Address and command are transmitted twice for reliability.

- > \* Pulse distance modulation.

- > \* Carrier frequency of 38kHz.

- > \* Bit time of 1.125ms or 2.25ms.

**Modulation:**

![](/media/da33571c6f0afb94b1ec1d91caba3edb.png)

The NEC protocol uses pulse distance encoding of the bits. Each pulse is
a 560µs long 38kHz carrier burst (about 21 cycles). A logical "1" takes
2.25ms to transmit, while a logical "0" is only half of that, being
1.125ms. The recommended carrier duty-cycle is 1/4 or 1/3.

**Protocol:**

![](/media/f970404e7bbfb5711fea5c776f689f3a.png)

The picture above shows a typical pulse train of the NEC protocol. With
this protocol the LSB is transmitted first. In this case Address $59 and
Command $16 is transmitted. A message is started by a 9ms AGC burst,
which was used to set the gain of the earlier IR receivers. This AGC
burst is then followed by a 4.5ms space, which is then followed by the
Address and Command. Address and Command are transmitted twice. The
second time all bits are inverted and can be used for verification of
the received message. The total transmission time is constant because
every bit is repeated with its inverted length. If you're not interested
in this reliability you can ignore the inverted values, or you can
expand the Address and Command to 16 bits each\!  
Keep in mind that one extra 560µs burst has to follow at the end of the
message in order to be able to determine the value of the last bit.

![](/media/63364daf21e5522c64eb8dfa82f2cef2.png)

A command is transmitted only once, even when the key on the remote
control remains pressed. Every 110ms a repeat code is transmitted for as
long as the key remains down. This repeat code is simply a 9ms AGC pulse
followed by a 2.25ms space and a 560µs burst.

![](/media/afea92a3b5cc1aa2457d2b118b157c84.png)

**Extended NEC protocol:**

The NEC protocol is so widely used that soon all possible addresses were
used up. By sacrificing the address redundancy the address range was
extended from 256 possible values to approximately 65000 different
values. This way the address range was extended from 8 bits to 16 bits
without changing any other property of the protocol.  
By extending the address range this way the total message time is no
longer constant. It now depends on the total number of 1's and 0's in
the message. If you want to keep the total message time constant you'll
have to make sure the number 1's in the address field is 8 (it
automatically means that the number of 0's is also 8). This will reduce
the maximum number of different addresses to just about 13000.

The command redundancy is still preserved. Therefore each address can
still handle 256 different commands.

![](/media/2f78d1ce7f001926f6b90ad966796e91.png)

Keep in mind that 256 address values of the extended protocol are
invalid because they are in fact normal NEC protocol addresses. Whenever
the low byte is the exact inverse of the high byte it is not a valid
extended address.

4. Decoded infrared signal：

We connect the infrared receiving element to the ESP32, according to the
wiring diagram below:

![](/media/700496cb1e0d5d23fd63c28469dd3fd0.png)

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
34：IR Control Sound and LED”. Select“irrecvdata.py”，right-click your
mouse to select“Upload to /”, wait for“irrecvdata.py” to be uploaded to
ESP32，and double left-click“Project\_34.1\_Decoded\_IR\_Signal.py”.

![](/media/129d42d4559af252c76a58de4591db66.png)

![](/media/1711de55644ddd6452348282a94a5fac.png)

    # Import the infrared decoder.
    from irrecvdata import irGetCMD
    
    # Associate the infrared decoder with GP0.
    recvPin = irGetCMD(0)
    
    #When infrared key value is obtained, print it out in"Shell". 
    try:
        while True:
            irValue = recvPin.ir_read() #Call ir_read() to read the value of the pressed key and assign it to IRValue.
            if irValue:
                print(irValue)
    except:
        pass

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”.

![](/media/6df2fc70b8f7f17d582d3d98ca9da654.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that aim the infrared remote control transmitter
at the infrared receiving head, press the button on the infrared
controller, and the "Shell" window of Thonny IDE prints the current
received key code values. Press“Ctrl+C”or
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to exit the program.

![](/media/039cc25496959e96d9a18702f4a6160a.png)

![](/media/623f8fa842b90a093d286954835483c6.png)

Write down the code associated with each button, because you will need
that information later.

![](/media/ebcf0cb2055f7784505f76ceeaef9f47.jpeg)

**5. Wiring diagram of the infrared remote control：**

![](/media/4912c1622e0eaedb76ea3a9b8ed969c0.png)

**6. Project code：**

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
34：IR Control Sound and LED”. Select“irrecvdata.py”，right-click your
mouse to select“Upload to /”,wait for“irrecvdata.py”to be uploaded to
ESP32，and double left-click
“Project\_34.2\_IR\_Control\_Sound\_And\_LED.py”.

![](/media/129d42d4559af252c76a58de4591db66.png)

![](/media/9bb11c32a178d3eecdd39d589226ebef.png)

    from machine import Pin,PWM
    import time
    from irrecvdata import irGetCMD
    
    #Set RGB light interface and frequency
    rgb_r = PWM(Pin(22))
    rgb_g = PWM(Pin(21))
    rgb_b = PWM(Pin(4))
    rgb_r.freq(1000)
    rgb_g.freq(1000)
    rgb_b.freq(1000)
    rgb_r.duty(0)
    rgb_g.duty(0)
    rgb_b.duty(0)
    # Initialize the buzzer pin 
    buzzer=Pin(15, Pin.OUT)
    
    #Configure infrared receiving pin and library
    recvPin = irGetCMD(0)
    
    while True:
        irValue = recvPin.ir_read() # Read remote control data
    # Determine whether there is a button that meets the needs 
        if irValue:
            print(irValue)
            buzzer.value(1)
            time.sleep(0.1)
            buzzer.value(0)
            if irValue == '0xff6897':   #1
               rgb_r.duty(1023)
               rgb_g.duty(0)
               rgb_b.duty(0)
               print('1')
            elif irValue == '0xff9867': #2
                rgb_r.duty(0)
                rgb_g.duty(1023)
                rgb_b.duty(0)
                print('2')
            elif irValue == '0xffb04f': #3
                rgb_r.duty(0)
                rgb_g.duty(0)
                rgb_b.duty(1023)
                print('3')
            elif irValue == '0xff30cf': #4
                rgb_r.duty(1023)
                rgb_g.duty(1023)
                rgb_b.duty(0)
                print('4')
            elif irValue == '0xff18e7': #5
                rgb_r.duty(1023)
                rgb_g.duty(0)
                rgb_b.duty(1023)
                print('5')
            elif irValue == '0xff7a85': #6
                rgb_r.duty(0)
                rgb_g.duty(1023)
                rgb_b.duty(1023)
                print('6')
            elif irValue == '0xff10ef': #7
                rgb_r.duty(1023)
                rgb_g.duty(1023)
                rgb_b.duty(1023)
                print('7') 
            else:
                rgb_r.duty(0)
                rgb_g.duty(0)
                rgb_b.duty(0)

7. Project result：

Make sure the ESP32 has been connected to the computer,
click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”.

![](/media/5351ebe3047b8f839753c5b4a6e6babb.png)

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and you'll see that press the 1 to 7 key of the infrared remote
controller, the buzzer will sound once, and the RGB light will be
red、green、blue、yellow、red、blue、green and white respectively. Press
another key (except 1 to 7 key), and the RGB light will go off.
Press“Ctrl+C”or click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”to
exit the program.

![](/media/be2580217f4eb6d530a065ed3c827a79.png)

**Note：When the code is running, the following prompt appears, you
just need to click![](/media/27451c8a9c13e29d02bc0f5831cfaf1f.png)“Stop/Restart backend”，then
click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script” to make the code run
again.

![](/media/3f425db5cda9eb56bc1f29c27fa6696d.png)

(Note: Before use, we need to remove the plastic sheet from the bottom
of the infrared remote controller.)

![](/media/3c9d76cb0d24d9861811ce2cb0bb6ae4.png)
