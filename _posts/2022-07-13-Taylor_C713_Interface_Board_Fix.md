---
title: "Headbanging: Hacking (fixing) the Taylor 063926-SER Interface Base Board"
date: 2022-07-13 12:00:00 +/-TTTT
image: https://calhoward.com/assets/img/2022/Taylor-C713-Interface-Board-Fix/07_13_2022_01-min.jpg
---

![]({{ site.baseurl }}/assets/img/2022/Taylor-C713-Interface-Board-Fix/07_13_2022_01-min.jpg)
*Pictured - Taylor 063926-SER "Interface Base Board"*

## Introducing *Headbanging*

This write-up is the first in my new series I'd like to call *Headbanging*. To kick off the series, join me on a circuitous adventure as I dive deep down the rabbit hole of repairing a 2011 model [Taylor](https://www.taylor-company.com/) C713 soft serve machine (yes, the notorious, ever-faulty, engineered-to-fail brand of machines known for being broken at McYouKnowWho's).

In this piece, I'll detail my one hell of a fix— a true hack, involving circuit modification— that I successfully performed on a faulty [C713](https://www.taylor-company.com/en/product-detail/model-c713) unit. 

Without further adeiu, the story and fix:

## Erratic behavior

After a particularly stormy summer weekend in coastal Georgia, I received a Monday morning service call about a broken soft serve machine. Thunderstorms always make me nervous, and afterwards I knew I was bound to hear from somebody with (now) faulty equipment. 

![]({{ site.baseurl }}/assets/img/2022/Taylor-C713-Interface-Board-Fix/07_13_2022_02-min.jpg)
*Stormy weather, the bane of electrical infrastucture - Photo credit: [Suparerg Suksai](https://www.pexels.com/@akedynamic/)*

**The issue: one side of the machine isn't dispensing anything, the other side won't shut off.**

*Great*, I think to myself, as I re-assure the panicked store manager everything will be fine. *I have no idea what's causing the issue or how to fix it.* 

Time to get digging.

## Isolating the issue

To solve issues on a soft serve machine, one must *think* like a soft serve machine. *Be* the soft serve machine. Okay, maybe soft serve machines don't have thoughts, but they do have hidden service menus. I enter my trusty access code, *5-2-3-1*, and access the "Manual Control" screen. 

Unsurprisingly, the machine does not respect my commands as I tell it to engage the left beater motor, or disengage the right beater motor. *Cool*, I think, *the machine has lost its mind*. It must be some combination of a shorted wire and blown fuse, maybe a bad relay, or contactor coil.

![]({{ site.baseurl }}/assets/img/2022/Taylor-C713-Interface-Board-Fix/07_13_2022_03-min.jpg)
*Pictured - the brains and circuitry of the C713*

I pop open the access panel and begin testing components. Lo and behold, everything passes. Dread sets in.

*Oh no*, I think, *it's the board. Something's fried.* In a ditch effort to confirm my suspicions, I transplant a known-working interface board from an adjacent machine into the faulty machine (a maniac move). Surprise, surprise: I confirm the issue is the interface board. 

This is problematic for several reasons: it's a proprietary part, meaning no off-the-shelf components can solve the issue, it's **expensive**, and waiting to get a replacement means that many days of lost potential in revenue for the store. And there's *two* fried interface boards.