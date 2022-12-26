# Project 36：WiFi AP Mode

1. Introduction：

ESP32 has three different WiFi operating modes : Station mode，AP
mode and AP+Station mode. All WiFi programming projects must be
configured with WiFi operating mode before using WiFi, otherwise
WiFi cannot be used. In this project, we will learn about ESP32's
WiFi AP mode.

2. Components：

|                        |                                 |
| ---------------------- | ------------------------------- |
| ![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg) |
| USB Cable\*1           | ESP32\*1                        |

3. Project wiring：

Connect the ESP32 to the USB port on your computer using a USB
cable.

![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg)

4. Component knowledge：

**AP mode :** When ESP32 selects AP mode, it creates a hotspot network
that is separated from the Internet and waits for other WiFi devices to
connect. As shown in the figure below, ESP32 is used as a hotspot. If a
mobile phone or PC wants to communicate with ESP32, it must be connected
to the hotspot of ESP32. Only after a connection is established with
ESP32 can they communicate.

![](/media/35d90f1ce10814ea1897ba63f8bd7ad9.png)

5. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
36：WiFi AP Mode”, and double left-click
“Project\_36\_WiFi\_AP\_Mode.py”.

![](/media/26df902f0cfa8aeb7664c3bf79b31866.png)

    import network #Import network module.
    
    #Enter correct router name and password.
    ssidAP         = 'ESP32_WiFi' #Enter the router name
    passwordAP     = '12345678'  #Enter the router password
    
    local_IP       = '192.168.1.147'
    gateway        = '192.168.1.1'
    subnet         = '255.255.255.0'
    dns            = '8.8.8.8'
    
    #Set ESP32 in AP mode.
    ap_if = network.WLAN(network.AP_IF)
    
    def AP_Setup(ssidAP,passwordAP):
        ap_if.ifconfig([local_IP,gateway,subnet,dns])
        print("Setting soft-AP  ... ")
        ap_if.config(essid=ssidAP,authmode=network.AUTH_WPA_WPA2_PSK, password=passwordAP)
        ap_if.active(True)
        print('Success, IP address:', ap_if.ifconfig())
        print("Setup End\n")
    
    try:
        AP_Setup(ssidAP,passwordAP)
    except:
        print("Failed, please disconnect the power and restart the operation.")
        ap_if.disconnect()

6. Project result：

Before the code runs, you can make any changes to the AP name and
password for ESP32 in the box as shown in the illustration above. Of
course, you can leave it alone by default.

Click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and open the AP function of ESP32 and print the access point
information in the "Shell" window of Thonny IDE.

![](/media/0bb4f0346021d20b9ed94f7dcf5c0392.png)

![](/media/5be2d032c8adcb2976c1640268919790.png)

Turn on the WiFi scanning function of your phone, and you can see the
ssid\_AP on ESP32, which is called "ESP32\_Wifi" in this code. You can
enter the password "12345678" to connect it or change its AP name and
password by modifying Code.

![](/media/3e0ad895bea7f5100cc02a415adcace7.png)
