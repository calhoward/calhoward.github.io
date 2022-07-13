---
title: "Taylor C713 Headbanging: Hacking (fixing) the 063926-SER Interface Base Board"
date: 2022-07-13 12:00:00 +/-TTTT
image: https://calhoward.com/assets/img/2022/Taylor-C713-Interface-Board-Fix/07_13_2022_01-min.jpg
---

![]({{ site.baseurl }}/assets/img/2022/Taylor-C713-Interface-Board-Fix/07_13_2022_01-min.jpg)
*Pictured - Taylor 063926-SER "Interface Base Board"*

## Preface

This write-up is the first in my new series I'd like to call, *Taylor C713 Headbanging*. Join me as I dive deep down the rabbit hole of repairing [Taylor](https://www.taylor-company.com/) soft serve machines (yes, the notorious, ever-faulty, engineered-to-fail brand of machines known for being broken at McYouKnowWho's).

To start off the series, I'd like to detail one hell of a fix— a true hack involving circuit modification— that I successfully performed on a faulty [C713](https://www.taylor-company.com/en/product-detail/model-c713) unit. 

## Erratic behavior

After a particularly stormy weekend in coastal Georgia, I receive a Monday morning service call about a broken soft serve machine. Thunderstorms always make me nervous, and afterwards I knew I was bound to hear from somebody with (now) faulty equipment. 

![]({{ site.baseurl }}/assets/img/2022/Taylor-C713-Interface-Board-Fix/07_13_2022_02-min.jpg)
*Stormy weather, the bane of electrical infrastucture - Photo credit: [Suparerg Suksai](https://www.pexels.com/@akedynamic/)*

**The issue: one side of the machine isn't dispensing anything, the other side won't shut off.**

*Great*, I think to myself, as I re-assure the panicked store manager everything will be fine. *I have no idea what's causing the issue or how to fix it.* Time to get digging.

## Isolating the issue

To solve issues on a soft serve machine, one must *think* like a soft serve machine. *Be* the soft serve machine. Okay, maybe soft serve machines don't have thoughts, but they do have hidden service menus. I enter my trusty access code, *5-2-3-1*, and access the "Manual Control" screen. 

Unsurprisingly, the machine does not respect my commands as I tell it to engage the left beater motor, or disengage the right beater motor. *Cool*, I think, *the machine has lost its mind*. It must be some combination of a shorted wire and blown fuse, maybe a bad relay, or contactor coil.

![]({{ site.baseurl }}/assets/img/2022/Taylor-C713-Interface-Board-Fix/07_13_2022_03-min.jpg)
*Pictured - the brains and circuitry of the C713*

I pop open the access panel and begin testing components. Lo and behold, everything passes. *Dread sets in.*

*Oh no*, I think, *it's the board. Something's fried.* In a ditch effort to confirm my awful suspicions (a maniac move), I transplant a known working interface board from an adjacent machine into the faulty machine. Surprise, surprise: we have two faulty interface boards.