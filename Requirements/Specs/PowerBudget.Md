# Power Budget

In this document we calculate the power-budget of the devices. First we stipulate that:
1. The overall device will consist out of a:
   1. Sensor
   2. 4G Transciever, with optional WiFi and 5G transcievers
   3. Micro-Controller
   4. Micro-Processor
   5. Power-Management chip that is able to power the board through direct current or battery. When connected to direct current, it should charge the battery
2. The Budget is calculated based on the runtime of 50 hours, as stipulated in the [Aanvullend Pig.docx](../SourceFiles/Aanvullend%20PiG.docx)
3. Has to fit into an enclosure that has the max. dimensions of:
   1. 250 mm * 150 mm * 80 mm
4. Max price of device is 500 euros, excluding sensors. 
5. IP 67 Certified Enclosure and connectors
6. Operational Temperature range of -20 degrees Celcius to +80 degrees Celcius 
7. With support for Dutch, German and the English Language. 


## Power Capacity based on enclosure
A first approximation of the Power budget will be the estimation of how many batteries will fit into the enclosure. For reference we use the widely adopted 18650 Li-ion battery, which has the follow specifics:
* Oprational Voltage: 3.7 Volts
* ~ 3000 mAh
* 11.1 Watt.Hours
* Dimensions: Diameter: 18 mm/ Length: 65mm/ Cubic Volume: 21.060 mm3

The enclosure has a max dimensions of 250mm * 150mm * 80 mm = 3.000.000 mm3. We can safely assume that we need about half of the space for components, leaving half of the enclosure available for batteries.
A volumentric approximation for the Power Density of the enclosure would be: 

total volume / volume of a single battery = capacity

Which means:

1.500.000 mm3 / 21.060 mm3/per battery = 71,2250 batteries

Which brings us to a capacity of:

11.1 Watt.Hours per Battery * ~ 70 Batteries = 777 Watt.Hours

This would be excessive for the application as it would assume 777 Watt.Hours / 50 hours = 15.54 Watt application. This would also be over budget, as a battery would approx. cost 10 euros, costing 700 euros, being 200 euros over the 500 euros budget. To add, a battery weighs in at about 46 grams, making the battery pack weigh in on 3,22 Kg for the batteries only. 

For reference, the power-draw under full load of embedded devices are listed below:
- Raspberry Pi 4 B: 6.4 Watts
- Raspberry Pi 3 B+: 5.1 Watts
- Raspberry Zero 2: 0.6 Watts
- ESP32 260 mA at 3.3 Volts = 0.033 mWatts - 0.858 Watts


Sources: [PiDramble](https://www.pidramble.com/wiki/benchmarks/power-consumption) and [lastminuteengineering](https://lastminuteengineers.com/esp32-sleep-modes-power-consumption/)

## Power Requirements 
In industrial applications it is seldomly chosen to extend the battery pack beyond 8 batteries. If we assume this to be the max. then we end up with 8 batteries * 11.1 Watt.Hours = 88.8 Watt.hours. Over a period of 50 Hours this would yield us about 1.776 Watts. This means that the bigger Raspberry Pi Models are not feasable and that the Raspberry Pi Zero 2 might not be feasible either, considerig that we need to account for the powerconsumption of other components like sensors, the non-trivial 4G Transciever and battery degredation. 

Based on 8 18650 Batteries, only a low-power micro-controller is possible. We therefore consider microcontrollers in the line of:
* ARM M0+ family as a very low power, low processing option
  * https://docs.arduino.cc/hardware/mkr-gsm-1400 
* ARM ESP32 family as feasibly high power, high processing option
  * https://www.amazon.de/-/nl/dp/B07VFPBRJ4/ref=sr_1_5?__mk_nl_NL=%C3%85M%C3%85%C5%BD%C3%95%C3%91&crid=1F0QF6GES2M1R&keywords=esp32+sim&qid=1654360656&s=ce-de&sprefix=esp32+sim%2Celectronics%2C78&sr=1-5
s