# Project 37：WiFi Station+AP Mode

1. Introduction：

ESP32 has three different WiFi operating modes : Station mode，AP
mode and AP+Station mode. All WiFi programming projects must be
configured with WiFi operating mode before using WiFi, otherwise
WiFi cannot be used. In this project, we will learn ESP32's WiFi
Station+AP mode.

2. Components：

|                        |                                 |
| ---------------------- | ------------------------------- |
| ![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg) |
| USB Cable\*1           | ESP32\*1                        |

3. Project wiring：

Connect the ESP32 to the USB port on your computer using a USB cable.

![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg)

4. Component knowledge：

**AP+Station mode:** In addition to AP mode and Station mode, ESP32 can
also use AP mode and Station mode at the same time. This mode contains
the functions of the previous two modes. Turn on ESP32's Station mode,
connect it to the router network, and it can communicate with the
Internet via the router. At the same time, turn on its AP mode to create
a hotspot network. Other WiFi devices can choose to connect to the
router network or the hotspot network to communicate with ESP32.

5. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
37：WiFi Station+AP Mode”，and double left-click
“Project\_37\_WiFi\_Station+AP\_Mode.py”.

![](/media/d01e07ffda5172e9a7162a1aa8977e89.png)

    import network #Import network module.
    
    ssidRouter     = 'ChinaNet-2.4G-0DF0' #Enter the router name
    passwordRouter = 'ChinaNet@233' #Enter the router password
    
    ssidAP         = 'ESP32_WiFi'#Enter the AP name
    passwordAP     = '12345678' #Enter the AP password
    
    local_IP       = '192.168.4.147'
    gateway        = '192.168.1.1'
    subnet         = '255.255.255.0'
    dns            = '8.8.8.8'
    
    sta_if = network.WLAN(network.STA_IF)
    ap_if = network.WLAN(network.AP_IF)
        
    def STA_Setup(ssidRouter,passwordRouter):
        print("Setting soft-STA  ... ")
        if not sta_if.isconnected():
            print('connecting to',ssidRouter)
            sta_if.active(True)
            sta_if.connect(ssidRouter,passwordRouter)
            while not sta_if.isconnected():
                pass
        print('Connected, IP address:', sta_if.ifconfig())
        print("Setup End")
        
    def AP_Setup(ssidAP,passwordAP):
        ap_if.ifconfig([local_IP,gateway,subnet,dns])
        print("Setting soft-AP  ... ")
        ap_if.config(essid=ssidAP,authmode=network.AUTH_WPA_WPA2_PSK, password=passwordAP)
        ap_if.active(True)
        print('Success, IP address:', ap_if.ifconfig())
        print("Setup End\n")
    
    try:
        AP_Setup(ssidAP,passwordAP)    
        STA_Setup(ssidRouter,passwordRouter)
    except:
        sta_if.disconnect()
        ap_if.idsconnect()



6. Project result：

It is analogous to Project 35 and project 36. Before running the code,
you need to modify ssidRouter, passwordRouter, ssidAP and passwordAP
shown in the box of the illustration above.

After making sure that the code is modified correctly,
click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script” the code starts to be
executed and the“Shell”window of Thonny IDE will display as follows:

![](/media/bda228850e629cd6bbceca628271548e.png)

![](/media/72c864c57de3f40d2a55ee3c10449898.png)

Turn on the WiFi scanning function of your phone, and you can see the
ssidAP on ESP32.

![](/media/3e0ad895bea7f5100cc02a415adcace7.png)
