---
title: Hacking the Leviton In-Wall Humidity Sensor & Fan Control
date: 2022-05-15 12:00:00 +/-TTTT
image: https://calhoward.com/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_01-min.jpg
---

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_01-min.jpg)
*The fully disassembled Leviton IPHS5-1LW*

## Introduction

>This post is a WIP, check back soon!
{: .prompt-tip }

>DANGER! This guide involves working with mains voltage wiring. Do not attempt to perform manual wiring on any of the circuits in your home. This guide is intended solely for educational purposes. 
{: .prompt-danger }

## Analyzing the board

The first step in reverse-engineering a circuit is to take a glance at the board and find the main logic ICs. In this case, the IPHS5-1LW uses the [Microchip](https://www.microchip.com/) [PIC15F1823 8-bit microcontroller IC](https://www.digikey.com/en/products/detail/microchip-technology/PIC16F1823-I-SL/2258580) as its main logic processor. For this project, the PIC16F1823 will be our target for analyzing logic and tapping into its I/O.

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_02-min.jpg)
*Fig. 1 - Photo of the IPHS5-1LW logic board*

Pictured above (*Fig. 1*) is a close-up shot of the low-voltage logic board found in the Leviton IPHS5-1LW. From this image, we can see several empty through-hole pads used for testing/probing in the factory where the board is assembled. These can be useful as probing points, as some of them are attached directly to the SMD pins on the PIC15F1823. 

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_06-min.jpg)
*PIC16F1823 pinout*

## Probing the circuit

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_03-min.jpg)
*Exposing the logic board while circuit is powered*

>CAUTION! Exposing live house wiring while also exposing live, disassembled wiring devices is extremely dangerous *and possibly lethal*. Do not do this.
{: .prompt-danger }

## Soldering in wires


![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_04-min.jpg)
*Holding the circuit and mod wires using helping-hand clamps*

## Buttoning it up

![]({{ site.baseurl }}/assets/img/2022/Hacking-Leviton-Fan-Humidity-Switch/05_15_2022_05-min.jpg)
*The fully packaged IPHS5-1LW with modded signal wires added*

## Refrences

[PIC16F1823 on DigiKey](https://www.digikey.com/en/products/detail/microchip-technology/PIC16F1823-I-SL/2258580)

[IPHS5-1LW on Leviton](https://www.leviton.com/en/products/iphs5-1lw)