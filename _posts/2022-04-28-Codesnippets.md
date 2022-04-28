---
title: Installing Hello on Debian 11
date: 2022-04-28 13:54:00 +/-TTTT
---


##Introduction

The GNU hello program produces a familiar, friendly greeting. It allows non-programmers to use a classic computer science tool which would otherwise be unavailable to them. 

##Updating the system

First, make sure your system is up to date.

Download updated package information from all configured sources:

``` bash
sudo apt update
```

Upgrade all installed packages to their latest versions:

``` bash
sudo apt upgrade
```
##Installing Hello

Next, install Hello:

``` bash
sudo apt install hello
```

That's it, we're done! Now, test the output of Hello:

``` bash
hello
Hello, world!
```

##Refrences
[GNU Hello](https://packages.debian.org/sid/hello)