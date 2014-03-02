---
layout: post
title:  "Reading digital input from Intel Galileo via linux sysfs interface"
date:   2014-03-01 23:45:00
categories: galileo
---

*This post is not about Arduino IDE - you need access to your Intel Galileo root console to be able to interact with it's filesystem.* 

First, connect your board to the push button as shown on [this diagram](http://arduino.cc/en/Tutorial/DigitalReadSerial) and power the board up.
 
Linux maps pins on the board to the filesystem under `/sys/class/gpio/`. It is not a straightforward mapping though, so PIN2 doesn't map to gpio2, but aparently to gpio14 and/or gpio32 (see [mappings](https://communities.intel.com/docs/DOC-21920)). Saying that I couldn't make it work, so let's move the input to PIN5 - that unconditionally is gpio17.

If you just booted your board, pin 17 is probably not visible in the filesystem at `/sys/class/gpio/gpio17/`. If that's the case you need to export it by calling

`# echo -n "17" > /sys/class/gpio/exports`

Now when you list `/sys/class/gpio/gpio17` you should be able to see directory structure simillar to this one:
 
`active_low  direction  drive  edge  power  subsystem  uevent  value`
 
The files that I was interested in are `direction` (whether it's a read "in" or write pin "out") and `value` ("0" or "1" for digital pins).
 
Now, we need to make sure, that gpio17 is in the "in" position and so ready to read the input from our button.

`# cat /sys/class/gpio/gpio17/direction`

if direction is "out" we need to change it, and it is as simple as writing to direction file like this:

`# echo -n "in" > //sys/class/gpio/gpio17/direction`

Now we are ready to read from it via:

`# cat /sys/class/gpio/gpio17/value`

... and when you press the button it should read "1", otherwise "0".
