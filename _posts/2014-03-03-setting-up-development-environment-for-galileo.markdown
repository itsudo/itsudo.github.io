---
layout: post
title:  "Setting up C development environment for Intel Galileo"
date:   2014-03-03 22:30:00
categories: galileo
---

*This post is work in progress*

  1. Read [Yocto Project Quick Start](https://www.yoctoproject.org/docs/current/yocto-project-qs/yocto-project-qs.html)
  2. Get sources for [Galileo IoT layer](http://git.yoctoproject.org/cgit/cgit.cgi/meta-intel-iot-devkit/)
  
    `git clone git://git.yoctoproject.org/meta-intel-iot-devkit`
    
  3. Compile images and devkit
    
    `source iot-devkit-init-build-env`
    
    `bitbake -c populate_sdk iot-devkit-prof-dev-image`
    
    If you are getting a bunch of errors from the start change DISTRO from "iot-devkit-locked" to "iot-devkit"
    
    
    
  4. Load image onto SD
  
  5. Setup devkit
    
    From build folder call
    
    `sh ./tmp/deploy/sdk/iot-devkit-eglibc-x86_64-iot-devkit-prof-dev-image-i586-toolchain-1.5.1.sh`
    
  6. Customize what goes onto the image (example with adding ruby)
  
  7. Setup wifi
    
    See [Sergey's blog post](http://www.malinov.com/Home/sergey-s-blog/intelgalileo-addingwifi)
