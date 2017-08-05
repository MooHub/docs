![](./logo-assets/moohub.png)

# Documentation
General documentation and tips for the project.

The first edition is based on ESP-01 , use a dht11 to take temperature and humidity ,and mini rele for a led 
ESP publish a responsive web page for read temp&humi , and control LED 

this version every 5 minuts put the read value on thingspeak

develop by 
* Mattia Moscheni [https://www.linkedin.com/in/moscheni]
* Salvatore Laisa [http://www.salvatorelaisa.me/]


... here some time can find a real project working http://raspberry.moscheni.it/sensor1

## Know bug 
*the developper*
*the beer* 

### Change log
0.1 first working test - **XX-08-2015**

0.1.1 start documentation - **03-10-2015**

### To Do List (pull requests are very welcomed)

## Install 




## Hardware TIPS 

#### test a new esp8266

Power on
It wasn’t simple. First I tried minicom with 115200 UART speed:

```minicom -b 115200 -o -D /dev/ttyUSB0```

This module display bootloader messages at 115200. After booting it switches to 9600. If you booted and can’t communicate but blue LED blinking when you type this may indicate that you need reset try
``` AT+RST<Ctrl-M><Ctrl-J> ```
You should get something like this:

``` 
[Vendor:www.ai-thinker.com Version:0.9.2.4] 
AT+GMR       // command for check FW version 
0018000902
OK
```

### make a Node step by step:


##### 1. Download the NodeMcu firmware
from here [Download nodemcu latest firmware](https://github.com/nodemcu/nodemcu-firmware/releases)
Can find two versions one with float enabled, and the other with float disabled only using integers.
Floating point uses more memory, not allowing code that worked on firmware builds without float enabled to load on float enabled firmware without memory issues.
*we use float integer version*

##### 2. Connect the ESP8266 module with a USB-Serial(TTL) convertor.

 Boot the module into “Download mode” by powering on with GPIO2 pulled up to VCC while GPIO0 and GPIO15 pulled down to GND (1K ~ 4.7K ohm resistors are required, don’t connect the pins to VCC/GND directly!).

##### 3. Write the firmware into ESP8266
can use [esptool.py](https://github.com/tommie/esptool) (a simple, platform independent, open source replacement for the offical XTCOM tool)
example for linux 

```./esptool.py write_flash 0x00000 nodelua_8266.fw```

or windows user can use this tool 
https://github.com/nodemcu/nodemcu-flasher


##### 4. Pull GPIO0 back to VCC, so the module will boot normally.
 Open a serial communication program minicom on Linux and Mac OS X, with command: 
 ```minicom -D /dev/ttyUSB0 -b 9600 -c on``` 
 or putty on MS Windows connect with baudrate 9600, then power on the module.

and test your device 
```
print(wifi.sta.getip())
--nil
wifi.setmode(wifi.STATION)
wifi.sta.config("SSID","password")
print(wifi.sta.getip())
--192.168.18.110
```

### License
Released under the MIT license.
