# Features / functions of this Buildroot configuration

This file describes the features/functions of the first working Buildroot configuration for the Santa Fe Opera e-libretto program.  The goal is to provide a tight kernel and OS image to run the functionality that we need.

This BuildRoot source is based and mirrored from the [latest official BuildRoot repo]( http://git.buildroot.net/buildroot/).  I'm using the ```2018.05.x``` branch of that repo.  *At the time of this writing, this is the most current stable release of BuildRoot.

At the time of writing, the SD Card image size is just under 400MB.  The target's root filesystem has 107M free.  We could make this bigger if our Serf programs get big, but it's unlikely too, really.

# Getting Started
```$BR```  the root of the BuildRoot tree that you checked out from Github.  For my lab machine, it's located at ```~/br/2018-05-v3-sfe```, created by issuing the following command from the ```~/br``` directory.  It was my third version of trying to do this, so that's why the v3, but feel free to use any directory name, obviously.

1. Clone the SFO BuildRoot repo:
```
 git clone git@github.com:santafeopera/buildroot.git 2018-05-v3-sfe
```

2. Type

# Misc Notes

## Networking

* DHCP works
* Hostname is "cm01" but you can change it by editing ```/etc/hostname```
* Bonjour/MDNS/Avahi works, so you can do ```ping cm01.local```
* OpenSSHD (and OpenSSH) are configured.  You can remote login to "cm01".
* Root password is ```asdfasdf```.
* SSH public keys are entered for my local NYC machines.  The place to add to this is in ```$BR/boards/raspberrypi3/rootfs_overlay/root/.ssh/authorized_keys```.  Then, the next time that you rebuild the kernel, you'll be able to login without a password.

## Misc Utilities Enabled (as requested by Scott)

* GPIO utilities
* RPi.GPIO Python library (WiringPi)
* bash
* ssh
* vim
* awk
* sed
* i2cdetect
    * *Binary works, but not sure if the i2c subsystem is functioning correctly. Haven't tested it out one way or the other.*
* iperf3

## Graphics

* The backlight automatically gets turned on at boot from the script located in ```/usr/local/bin/sfo_backlight```.  If no parameters are provided to the script, then 50% is assumed.

### PyQT5
* PyQt5 works. See the ```/root/pyqt5-test``` directory for a test.
* The QT5 variables defining the screen resolution and size are defined in the file ```/root/.qt5-env.sh``` which is sourced by ```/root/.profile```.

### Cross Compiling C++ Qt5

* There is no compiler on the target Carrier Board system.  All compilation must be done on the x86 HOST Ubuntu machine.

* I haven't looked into cross-compiling a Qt5 C++ program yet.  [This is a good reference page](http://www.jumpnowtek.com/rpi/Raspberry-Pi-Systems-with-Buildroot.html), and specifically, the section on ```Using the Buildroot cross-toolchain``` towards the end of that page.  I've cross compiled a hello world (shell only, not Qt) on my x85 Ubuntu box and it worked well on the CB.

* There's a simple Hello-World C program that is build using the cross compiler that BuildRoot generates.  The C source and makefile are located in ```$BR/board/raspberrypi3/src/hwc```.

  Note that the compiler that the Makefile uses is the cross-compiler, and it's located at ```$BR/output/host/usr/bin/arm-linux-gcc```.

  All of the cross-compiler libraries, includes and binaries are located in the ```$BR/output/host``` directory, so I suspect that you can just follow the same pattern as in the simple ```hwc``` example.

## Touchscreen

* I have not gotten the touchscreen to work yet.  Haven't really tried.  That's next on my list, most likely after some help from Scott.

# Near Futures

* Turns out that ```ZeroMQ``` as well as the multi-cast ```NORM``` protocol have pre-built packages in the latest BuildRoot release (which is the one that this is built on).  I'll be working on getting that right.

* Before too long, I'll reconfigure this Buildroot setup to be proper.  We'll have our own ```$BR/boards/santafeopera/``` directory instead of building out of the directory ```$BR/boards/raspberrypi3``` like we currently do.

# TTD:
