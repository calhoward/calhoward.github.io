---
title: Installing openMAINT 3.4 on Debian 11 "Bullseye"
date: 2022-04-29 10:48:00 +/-TTTT
image: https://calhoward.com/assets/img/2022/pexels-kateryna-babaieva-2760241-Cropped-min.jpg
---

*Photo credit - [Kateryna Babaieva](https://www.pexels.com/@kateryna-babaieva-1423213/)*

## Introduction

[openMAINT](https://www.openmaint.org/en) is a ready-to-use CMMS program (Computerized Maintenance Management System) created and maintained by [Tecnoteca Srl](https://www.tecnoteca.com/). It is a powerful tool that, when configured to suit the needs of your enterprise, can transform the way you organaize and manage your work. openMAINT is a "verticalized" solution built on top of [CMDBuild](https://www.cmdbuild.org/en/homepage), also maintained by Tecnoteca, Srl.

Check out Tecnoteca's [What is openMAINT](https://www.openmaint.org/en/product/project) page to learn more about the project, or request a [demo](https://www.openmaint.org/en/contacts/request-demo) to see if openMAINT might work for you.

## Installing the base system

![]({{ site.baseurl }}/assets/img/2022/pexels-field-engineer-442152-Cropped-min.jpg)
*Photo credit - [Field Engineer](https://www.pexels.com/@field-engineer-147254/)*

To continue, we will assume you have already installed a fresh copy of [Debian 11 "Bullseye" (stable)](https://www.debian.org/releases/stable/) running [openssh-server](https://packages.debian.org/bullseye/openssh-server) (or your preferred SSH server of choice), with root access enabled. A desktop environment is not required to set up an openMAINT server. 

Follow [my guide on installing Debian 11](https://calhoward.com/2022-04-28-Installing_Debian11) if you're unsure of how to get a Debian system up and running. Also, follow my [other guide on installing and setting up a SSH server](https://calhoward.com/2022-04-28-Installing_openssh-server_Debian11) if you're unsure of how to do that.

Once the above requirements are satisfied and you are able to remotely connect to your Debian server, continue to the next step.

## Logging in for the first time

We will mainly be interacting with our server by using the SSH protocol. From any terminal, use the `ssh` command to log in with the user you created while setting up Debian. In our case, I've named the user `openmaint`:

``` bash
ssh openmaint@<server_ip>
```

Make sure your user has access to sudo privileges by issuing the `whoami` command. The console should return `root`:

``` bash
sudo whoami
```
```
We trust you have received the usual lecture from the local System
Administrator. It usually boils down to these three things:

    #1) Respect the privacy of others.
    #2) Think before you type.
    #3) With great power comes great responsibility.

[sudo] password for openmaint:
root
```
## Updating the system

Before we install any software, make sure your system is up to date. We will accomplish this by running `apt update` & `apt upgrade`. Use the `-y` flag to save time and skip "yes" prompts.

Download updated package information from all configured sources:

``` bash
sudo apt update -y
```

Upgrade all installed packages to their latest versions:

``` bash
sudo apt upgrade -y
```

## Installing utilities

In order to bring about the successful installation of openMAINT (and all its dependencies), we will be working with a few commandline utilities. These utilities are [gnupg2](https://packages.debian.org/bullseye/gnupg2), [wget](https://packages.debian.org/bullseye/wget), [unzip](https://packages.debian.org/bullseye/unzip), [git](https://packages.debian.org/bullseye/git), [curl](https://packages.debian.org/bullseye/curl), and [nano](https://packages.debian.org/bullseye/nano).

Install them all simultaneously with the following single command. Use the `-y` flag to save time and skip "yes" prompts:

```bash
sudo apt install -y gnupg2 wget unzip git curl nano
```


## Installing dependencies

Now that our system is up-to-date, it is time to install dependencies required by openMAINT 3.4. Use the `-y` flag to save time and skip "yes" prompts.

[openjdk-17-jdk](https://packages.debian.org/bullseye/openjdk-17-jdk):

```bash
sudo apt install -y openjdk-17-jdk
```

To make sure OpenJDK 17 has been installed correctly, and that your `$JAVA_HOME` environment variable is correctly configured, use the `java -version` command:

```bash
java -version
```
```
openjdk version "17.0.2" 2022-01-18
OpenJDK Runtime Environment (build 17.0.2+8-Debian-1deb11u1)
OpenJDK 64-Bit Server VM (build 17.0.2+8-Debian-1deb11u1, mixed mode, sharing)
```

At the time of writing, the most up-to-date build is 17.0.2. If you don't see at least version 17.x.x, you may have to configure alternatives for Java:

```bash
sudo update-alternatives --config java
```
```
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                         Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-17-openjdk-amd64/bin/java   1711      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java   1111      manual mode
  2            /usr/lib/jvm/java-17-openjdk-amd64/bin/java   1711      manual mode

Press <enter> to keep the current choice[*], or type selection number:
```

In my case, I also had OpenJDK 11 installed. Simply type the correct number and press `<enter>`.

```
0
update-alternatives: using /usr/lib/jvm/java-17-openjdk-amd64/bin/java to provide /usr/bin/java (java) in auto mode
```

Next, we must add PostgreSQL repos to our sources list.

Run the following command to install the [GPG key](https://wiki.debian.org/GnuPG):

```bash
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
```
```
Warning: apt-key is deprecated. Manage keyring files in trusted.gpg.d instead (see apt-key(8)).
OK
```

Next, add PostgreSQL repository to your apt sources:

```bash
echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" |sudo tee  /etc/apt/sources.list.d/pgdg.list
```
```
deb http://apt.postgresql.org/pub/repos/apt/ bullseye-pgdg main
```

Update your system. Use the `-y` flag to save time and skip "yes" prompts:

```bash
sudo apt update -y
```

Finally, install PostgreSQL. Use the `-y` flag to save time and skip "yes" prompts:

```bash
sudo apt install -y postgresql-13 postgresql-client-10 postgresql-10-postgis-3 libpostgis-java
```

Once PostgreSQL is installed, it is time to pick a strong password and apply it to the user `postgres`.

Use `passwd` to set your new strong password:

```bash
sudo passwd postgres
```
```
New password:
Retype new password:
passwd: password updated successfully
```
Next, we must update the postgres role with the new password. Use the `su` (switch user) command to switch to the `postgres` user:

```bash
su - postgres
```
```
Password:
```

Use `psql` to alter the password for postgres:

```bash
psql -d template1 -c "ALTER USER postgres WITH PASSWORD 'StrongPassword';"
```
```
ALTER ROLE
```

Then type `exit` to log out:
```bash
exit
```
```
logout
```
## Installing openMAINT

Now that openMAINT's dependencies are installed and properly configured, we can now move forward and install openMAINT.

Use `wget` to download the latest `.war` file for openMAINT. At the time of writing, the latest version is [openmaint-2.2-3.4](https://sourceforge.net/projects/openmaint/files/2.2/Core%20updates/openmaint-2.2-3.4/).

```bash
wget https://sourceforge.net/projects/openmaint/files/2.2/Core%20updates/openmaint-2.2-3.4/openmaint-2.2-3.4.war
```
Now, execute the install script with java:

```bash
java -jar openmaint-2.2-3.4.war install
```

Follow through the prompts. You may leave all of the defaults as they are by pressing `<enter>` on each line. Make sure you enter your strong password you created for the `postgres` user.

```
CMDBuild interactive install wizard - welcome!

this wizard will guide you in the process of installing and configuring a new instance of CMDBuild!
```

Press `<enter>` to leave the default install location:

```
tomcat install location </home/openmaint/cmdbuild_30> :
```

Press `<enter>` to leave the default http port:

```
tomcat http port <8080>:
```

Press `<enter>` to leave the default shutdown port:

```
tomcat shutdown port (offset already applied) <8005>:
```

Press `<enter>` to leave the default debug port:

```
tomcat debug port (offset already applied) <8000>:
```

Press `<enter>` to leave the default postgres database host/port:

```
postrgres db <localhost:5432> : 
```

Input your strong password for the `postgres` user:

```
postrgres admin account <postgres/postgres> : postgres/StrongPassword
```

Press `<enter>` to leave the default database name:

```
WARNING: server version 10.20 is not supported, you may encounter problems
cmdbuild posrgres database name <cmdbuild_a70b> :
```

To initialize openMAINT with a blank database, load `empty.dump.xz`:

```
database dump to load <demo> : empty.dump.xz
```

Look over your inputs and verify the configuration is correct:

```
we're ready to begin, this is your configuration:

         tomcat: /home/openmaint/cmdbuild_30
         http port: 8080
         shutdown port: 8005
         debug port: 8000
         postgres database: localhost:5432/cmdbuild_a70b
         database dump: empty.dump.xz

if everything is ok, press ENTER to begin installation
<press enter to begin>
```

Press `<enter>` to begin installation:

```
BEGIN installation
install tomcat...
OK
create database...
create database cmdbuild_a70b empty.dump.xz
apply patches
adjust configs
done
OK


cmdbuild successfully installed! you can find startup/shutdown scripts in dir /home/openmaint/cmdbuild_30/bin
```

openMAINT and its dependencies are now successfully installed.

## Starting openMAINT

Now that openMAINT and its dependencies are installed, it is time to start the server up. Navigate to the `bin` directory to find the startup script:

```bash
cd ~/cmdbuild_30/bin
```

Run `startup.sh`:

```bash
./startup.sh
```

```
Using CATALINA_BASE:   /home/openmaint/cmdbuild_30
Using CATALINA_HOME:   /home/openmaint/cmdbuild_30
Using CATALINA_TMPDIR: /home/openmaint/cmdbuild_30/temp
Using JRE_HOME:        /usr
Using CLASSPATH:       /home/openmaint/cmdbuild_30/bin/bootstrap.jar:/home/openmaint/cmdbuild_30/bin/tomcat-juli.jar
Using CATALINA_OPTS:
Using CATALINA_PID:    /home/openmaint/cmdbuild_30/bin/catalina.pid
Tomcat started.
```

That's it! openMAINT is now running on your local server and is accessible via `http://<server-ip>:8080/cmdbuild/ui`.

For further reading, check out my other guide [Securing Your openMAINT Server on Debian 11 with SSL](https://calhoward.com/2022-04-29-Securing_openMAINT_Debian11_SSL). 

For help onboarding, see [Onboarding openMAINT 3.4](https://calhoward.com/2022-04-29-Onboarding_openMAINT3.4).




## Disclaimer

*I am not affiliated with Tecnoteca Srl., nor am I maintainer of either openMAINT, or CMDBuild. This guide is written in good faith, and in the spirit of contribution towards the Free Software Movement, for consumption as-is.*

*Some of the steps listed in this guide may break or cease to function as software packages are updated, deprecated, or become obseleted.*
## Refrences

[openMAINT on SourceForge](https://sourceforge.net/projects/openmaint/)

[openmaint.org](https://www.openmaint.org/)
