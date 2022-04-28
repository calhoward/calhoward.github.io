---
title: Installing Hello on Debian 11
date: 2022-04-28 13:54:00 +/-TTTT
---

The GNU hello program produces a familiar, friendly greeting. It allows non-programmers to use a classic computer science tool which would otherwise be unavailable to them. 

To install hello on Debian 11, perform the following steps:

Download updated package information from all configured sources:

``` bash
sudo apt update
```

Upgrade all installed packages to their latest versions:

``` bash
sudo apt upgrade
```

Next, install Hello:

``` bash
sudo apt install hello
```

That's it, we're done! Now, test the output of Hello:

``` bash
hello
Hello, world!
```

This post was created to test Rouge code snippets and syntax highlighting for Jekyll.