---
title: Installing GNU Hello on Debian 11
date: 2022-04-28 13:54:00 +/-TTTT
image: {{ site.baseurl }}/assets/img/2022/pexels-pixabay-207580_cropped16_9.jpg
---

![]({{ site.baseurl }}/assets/img/2022/pexels-pixabay-207580_cropped16_9.jpg)
*Photo credit - [Pixabay](https://www.pexels.com/@pixabay/)*

## Introduction

The GNU hello program produces a familiar, friendly greeting. It allows non-programmers to use a classic computer science tool which would otherwise be unavailable to them. 

This tutorial is written for Debian 11, however this process should work for most Debian or Ubuntu based systems. Follow along to learn how to install GNU Hello.

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
## Installing Hello

Next, install Hello:

``` bash
sudo apt install hello
```

That's it, we're done! Now, test the output of Hello:

``` bash
hello
Hello, world!
```

## Refrences
[GNU Hello](https://packages.debian.org/sid/hello)