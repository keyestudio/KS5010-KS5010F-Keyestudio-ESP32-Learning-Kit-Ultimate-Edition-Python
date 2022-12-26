# Project 35：WiFi Station Mode

1. Introduction：

ESP32 has three different WiFi operating modes : Station mode，AP mode
and AP+Station mode. All WiFi programming projects must be configured
with WiFi operating mode before using WiFi, otherwise WiFi cannot be
used. In this project, we will learn about ESP32's WiFi Station mode.

2. Components：

|                        |                                 |
| ---------------------- | ------------------------------- |
| ![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg) |
| USB Cable\*1           | ESP32\*1                        |

3. Project wiring：

Connect the ESP32 to the USB port on your computer using a USB cable.

![](/media/53f17b0de2d98d4714e8fe9043a346ca.jpeg)

4. Component knowledge：

**Station mode:** When ESP32 selects Station mode, it acts as a WiFi
client. It can connect to the router network and communicate with other
devices on the router via WiFi connection. As shown below, the PC is
connected to the router, and if ESP32 wants to communicate with the PC,
it needs to be connected to the router.

![](/media/f74baff97695aa2ee33a8c19370d2547.png)

5. Project code：

Codes used in this tutorial are saved in“**2. Windows System\\1.
Python\_Tutorial\\2. Python Projects**”. You can move the codes to any
location. For example, we save the codes in Disk(D) with the path of
“D:\\2. Python Projects”.

![](/media/906b7d4391131929a6b0726f7f5bab30.png)

Open“Thonny”，click“This computer”→“D:”→“2. Python Projects”→“Project
35：WiFi Station Mode”，and double left-click
“Project\_35\_WiFi\_Station\_Mode.py”.

![](/media/11923944980577ce6e633ca4b7b0c6c6.png)

    import time
    import network # Import network module.
    
    ssidRouter     = 'ChinaNet-2.4G-0DF0' # Enter the router name
    passwordRouter = 'ChinaNet@233' # Enter the router password
    
    def STA_Setup(ssidRouter,passwordRouter):
        print("Setup start")
        sta_if = network.WLAN(network.STA_IF) # Set ESP32 in Station mode.
        if not sta_if.isconnected():
            print('connecting to',ssidRouter)
      # Activate ESP32’s Station mode, initiate a connection request to the router
      # and enter the password to connect.      
            sta_if.active(True)
            sta_if.connect(ssidRouter,passwordRouter)
      #Wait for ESP32 to connect to router until they connect to each other successfully.      
            while not sta_if.isconnected():
                pass
      # Print the IP address assigned to ESP32-WROVER in “Shell”. 
        print('Connected, IP address:', sta_if.ifconfig())
        print("Setup End")
    
    try:
        STA_Setup(ssidRouter,passwordRouter)
    except:
        sta_if.disconnect()

6. Project result：

Because the names and passwords of routers in various places are
different, before the code runs, users need to enter the correct
router’s name and password in the box as shown in the illustration
above.

After making sure the router name and password are entered correctly,
click![](/media/da852227207616ccd9aff28f19e02690.png)“Run current script”, the code starts to be
executed and wait for ESP32 to connect to your router and print the IP
address assigned by the router to ESP32 in the "Shell" window of Thonny
IDE.

![](/media/9fd5207ee2a5e6329a1d5ac40a16ba58.png)

![](/media/e283d185859ce0a4372c53449bfd03b8.png)
