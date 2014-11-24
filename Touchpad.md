ELAN PS2 Touchpad fix
========================

### Get synaptics driver for X11

Edit make.conf, set INPUT_DEVICE
````
INPUT_DEVICE="evdev synaptics"
````
this will pull both ELAN and Synaptics driver

### Modify evdev.conf
Edit X11's evdev.conf, so it will use synaptics driver for touchpad
````
vim /etc/X11/xorg.conf.d/10-evdev.conf
````
Create this file if it does not exist,
Change `Driver "evdev"` to `Driver "synaptics"`
````
Section "InputClass"
	Identifier "evdev touchpad catchall"
	MatchIsTouchpad "on"
	MatchDevicePath "/dev/input/event*"
	Driver "synaptics"
EndSection
````
This should provide basic touchpad capabilities like two-finger scroll

### Personalize

You can personalize the touchpad with more options.

Run `synclient` to see the available options and values



##### My setting:

`TapButton1=1` Tap with 1 finger: left-click

`SingleTapTimeout=0` Tap will immediately create event



Theoretically, this fix should also work for Mac OS X, in case you want a hackintosh.
