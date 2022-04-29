---
title: Installing openMAINT 3.4 on Debian 11 "Bullseye"
date: 2022-04-29 10:48:00 +/-TTTT
---

![]({{ site.baseurl }}/assets/img/2022/pexels-kateryna-babaieva-2760241_cropped16_9.jpg)
*Photo credit - [Kateryna Babaieva](https://www.pexels.com/@kateryna-babaieva-1423213/)*

## Introduction

[openMAINT](https://www.openmaint.org/en) is a ready-to-use CMMS program (Computerized Maintenance Management System) created and maintained by [Tecnoteca Srl](https://www.tecnoteca.com/). It is a powerful tool that, when configured to suit the needs of your enterprise, can transform the way you organaize and manage your work. openMAINT is a "verticalized" solution built on top of [CMDBuild](https://www.cmdbuild.org/en/homepage), also maintained by Tecnoteca, Srl.

Check out Tecnoteca's [What is openMAINT](https://www.openmaint.org/en/product/project) page to learn more about the project, or request a [demo](https://www.openmaint.org/en/contacts/request-demo) to see if openMAINT might work for you.

## Installing the base system

![]({{ site.baseurl }}/assets/img/2022/pexels-field-engineer-442152_Cropped.jpg)
*Photo credit - [Field Engineer](https://www.pexels.com/@field-engineer-147254/)*

To continue, we will assume you have already installed a fresh copy of [Debian 11 "Bullseye" (stable)](https://www.debian.org/releases/stable/) running [openssh-server](https://packages.debian.org/bullseye/openssh-server) (or your preferred SSH server of choice), with root access enabled. A desktop environment is not required to set up an openMAINT server. 

Follow [my guide on installing Debian 11](https://calhoward.com/2022-04-28-Installing_Debian11) if you're unsure of how to get a Debian system up and running. Also, follow my [other guide on installing and setting up a SSH server](https://calhoward.com/2022-04-28-Installing_openssh-server_Debian11) if you're unsure of how to do that.

Once the above requirements are satisfied and you are able to remotely connect to your Debian server, continue to the next step.

## Updating the system

First, make sure your system is up to date. We will accomplish this by running apt update & apt upgrade.

Log in to your server using the account you created while setting up Debian. In our case, I've named the user "openmaint". 

``` bash
ssh openmaint@<server_ip>
```

Download updated package information from all configured sources:

``` bash
sudo apt update
```

Upgrade all installed packages to their latest versions:

``` bash
sudo apt upgrade
```
## Installing Dependencies

Next, install:

``` bash
sudo apt install 
```

## Disclaimer

*I am not affiliated with Tecnoteca Srl., nor am I maintainer of either openMAINT, or CMDBuild. This guide is written in good faith, and in the spirit of contribution towards the Free Software Movement, for consumption as-is.*

*Some of the steps listed in this guide may break or cease to function as software packages are updated, deprecated, or become obseleted.*
## Refrences

[openMAINT on SourceForge](https://sourceforge.net/projects/openmaint/)

[openmaint.org](https://www.openmaint.org/)