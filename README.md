ChargeGuru
=====
This is an application to control SkyRC B6* chargers. It's a replacement for the ChargeMaster application
provided by the manufacturer, which is badly designed and doesn't work on GNU/Linux. It's written in Qt5.

![screenshot](https://i.imgur.com/SSo5eYT.png)

Installation
------------
Dependencies:
```
qt5 qtcharts libusb-1.0 libb6
```

Grab `libb6` from https://github.com/maciek134/libb6.

in .bashrc add:
```bash
export Qt5Core_DIR="/home/wiktor-lyncas/Qt/5.15.2/gcc_64/lib/cmake/Qt5Core/"
export Qt5Gui_DIR="/home/wiktor-lyncas/Qt/5.15.2/gcc_64/lib/cmake/Qt5Gui/"
export Qt5Widgets_DIR="/home/wiktor-lyncas/Qt/5.15.2/gcc_64/lib/cmake/Qt5Widgets/"
export Qt5Charts_DIR="/home/wiktor-lyncas/Qt/5.15.2/gcc_64/lib/cmake/Qt5Charts/"
```

Run these commands to compile the software:
```bash
$ mkdir build
$ cd build
$ cmake .. -DCMAKE_BUILD_TYPE=Release
$ make
```

Either run the programs that use it as root (**not recommended**) or create an udev rule similar to this one:
```udev
SUBSYSTEM=="usb", ATTRS{idVendor}=="0000", ATTRS{idProduct}=="0001", MODE:="666", GROUP="plugdev"
KERNEL=="hidraw*", ATTRS{idVendor}=="0000", ATTRS{idProduct}=="0001", MODE="0666", GROUP="plugdev"
```

Start the software and connect the charger, the interface will be enabled when charger's interface is up (it may take a few seconds, the MCU is a bit slow in that aspect).

What's working
--------------
- [x] device information
- [x] system settings
- [x] starting / stopping charging with all available options
- [x] toggable charging charts
- [x] displaying charging errors
- [x] notification after charging complete

TODO / what to expect in the future
-----------------------------------
- [ ] saving charging profiles for quick use
- [ ] battery datasheet / charging profile database
- [ ] charging data export (to `csv`)
- [ ] pause / resume charging
- [ ] SMS / e-mail notifications
- [ ] touch interface?
- [ ] Windows build if I figure out how to make CMake work in there
