---
title: Installing openMAINT 3.4 on Debian 11
date: 2022-04-29 10:48:00 +/-TTTT
---

![]({{ site.baseurl }}/assets/img/2022/pexels-kateryna-babaieva-2760241_cropped16_9.jpg)

## Introduction

[openMAINT](https://www.openmaint.org/en) is a ready-to-use CMMS program (Computerized Maintenance Management System) created and maintained by [Tecnoteca Srl](https://www.tecnoteca.com/). It is a powerful tool that, when configured to suit the needs of your enterprise, can transform the way you organaize and manage your work. openMAINT is a "verticalized" solution built atop [CMDBuild](https://www.cmdbuild.org/en/homepage), also maintained by Tecnoteca, Srl.

Check out Tecnoteca's [What is openMAINT](https://www.openmaint.org/en/product/project) page to learn more about the project, or request a [demo](https://www.openmaint.org/en/contacts/request-demo) to see if openMAINT might work for you.

## Installing the base system

![]({{ site.baseurl }}/assets/img/2022/pexels-field-engineer-442152_Cropped.jpg)

To continue, we will assume you have already installed a fresh copy of [Debian 11 "Bullseye" (stable)](https://www.debian.org/releases/stable/) running [openssh-server](https://packages.debian.org/bullseye/openssh-server) (or your preferred SSH server of choice), with root access enabled. A desktop environment is not required to set up an openMAINT server. 

Once the above requirements are satisfied and you are able to remotely connect to your Debian server, continue to the next step.

## Updating the system

First, make sure your system is up to date. We will accomplish this by running apt update & apt upgrade.

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


## Refrences

[openMAINT on SourceForge](https://sourceforge.net/projects/openmaint/)

[openmaint.org](https://www.openmaint.org/)