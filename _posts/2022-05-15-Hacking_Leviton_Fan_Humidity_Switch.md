---
title: Hacking the Leviton IPHS5-1LW In-Wall Humidity Sensor & Fan Control and Adding WiFi Connectivity & Control
date: 2022-05-15 12:00:00 +/-TTTT
image: https://calhoward.com/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_01-min.jpg
---

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_01-min.jpg)
*The fully disassembled Leviton IPHS5-1LW*

## Introduction

>This post is a WIP, check back soon!
{: .prompt-tip }

>!! DANGER !! This guide involves working with AC mains voltage wiring. Do not attempt to perform manual wiring on any of the circuits in your home. This guide is intended solely for educational purposes. 
{: .prompt-danger }

## Analyzing the board

The first step in reverse-engineering a circuit is to take a glance at the board and find the main logic ICs. In this case, I identified the [Microchip](https://www.microchip.com/) [PIC16F1823 8-bit microcontroller IC](https://www.digikey.com/en/products/detail/microchip-technology/PIC16F1823-I-SL/2258580) as the main logic processor used in the IPHS5-1LW. For this project, the PIC16F1823 will be our target for analyzing the circuit's logic, as well as tapping into and controlling its I/O.

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_02-min.jpg)
*Fig. 1 - Photo of the IPHS5-1LW logic board*

Pictured above (*Fig. 1*) is a close-up shot of the low-voltage logic board found in the Leviton IPHS5-1LW. The larger 14-pin IC in the top-right is the PIC16F1823. From this image, we can see several empty through-hole pads used for testing/probing in the factory where the board is assembled. These can be useful as probing points, as some of these have traces leading directly to the SMD pins on the PIC15F1823. 

Of course, the [datasheet](https://ww1.microchip.com/downloads/en/DeviceDoc/PIC12LF1822-16LF1823-Data-Sheet-40001413F.pdf) will tell us everything we need to know about each of the the I/O pins, as shown in the following diagram and chart pulled from the datasheet:

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_06-min.jpg)
*Fig. 2 - PIC16F1823 pinout*

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_07-min.jpg)
*Fig. 3 - PIC16F1823 pin allocation table*

This key shows us where the power pins, `VSS` (voltage source) and `VDD` (voltage drain), are located. From here, we just need to isolate the pins that are responsible for the logic of the relay driver and for the logic of the activation button. To do this, we will have to test probe the circuit while it is live.

## Probing the circuit

>!! DANGER !! Exposing live house wiring while also exposing live, disassembled AC wiring devices is extremely dangerous *and possibly lethal*. Do not do this.
{: .prompt-danger }

To locate the pins that control the fan and the button, I used my digital multimeter set to DC voltage to listen for the 3.3v logic on each general-purpose I/O pin, taking note of which pin I'm on by refrencing the pinout diagram and pin allocation diagram. 

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_03-min.jpg)
*Exposing the logic board while circuit is powered*

After careful probing, I found the fan control logic output at `RC5`. This pin normally outputs 0.0v (`low`) while the fan is off, and outputs 3.3v (`high`) when the fan is running. After further careful probing, I found the button logic pin at `RA0`. This pin normally outputs 3.3v (`high`), and changes to 0.0v (`low`) when the button is closed/depressed. 

With the logic found and analyzed, it's time to move on to the next step, soldering in our mod wires.

## Soldering in wires

For ease and for modularity's sake, I opted to use male pin header jumper wires (with one end cut off for board soldering) to connect to the logic board. These male header pins will be ran out through the side of the black plastic case that houses the logic and relay board in the IPHS5-1LW, making use of the factory cutout. 

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_04-min.jpg)
*Holding the circuit and mod wires using helping-hand clamps*

After careful soldering to `VSS`, `VDD` and `RA0` via the through-hole pads, as well as `RC5` via direct solder to the SMD pin of the IC, our little header wire is ready for action. All that's left is to re-assemble the case and start interfacing with the switch.

## Buttoning it up

Voilà! The IPHS5-1LW is fully re-assembled and with exposed headers to leads `VSS` (3v3), `VDD` (ground), `RA0` (button), and `RC5` (fan relay driver)on the PIC15F1823 microcontroller.

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_05-min.jpg)
*The fully packaged IPHS5-1LW with modded signal wires added*

With the relevant logic channels exposed, the next step is to use the exposed channels to interface with an [ESP8266](https://www.espressif.com/en/products/socs/esp8266) board in order to achieve control of the circuit via WiFi. 

## To be continued...

This guide will be expanded to include ESP8266 programming and adding WiFi control in the future. Check back soon.
## Refrences

[PIC16F1823 on DigiKey](https://www.digikey.com/en/products/detail/microchip-technology/PIC16F1823-I-SL/2258580)

[IPHS5-1LW on Leviton](https://www.leviton.com/en/products/iphs5-1lw)