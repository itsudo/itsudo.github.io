---
layout: post
title:  "Customizing what goes onto yocto image"
date:   2014-03-05 14:30:00
categories: galileo yocto ruby
---

*This post is work in progress*

I will try to explain how to customize what goes onto your image. As an example I will use ruby that I want to make available on my intel galileo board.

If you are not familiar with basics of building an image, see [this post](http://www.itsudo.com/galileo/2014/03/03/setting-up-development-environment-for-galileo.html)

  1. Finding meta package
    
    Good start http://layers.openembedded.org/layerindex/branch/master/layers/
    
    So I'll clone OpenEmbedded git repo with `git clone git://git.openembedded.org/meta-openembedded`
  
  2. Add new layers to your config
    
    Add absolute path to `meta-ruby` to conf/bblayers.conf. Unfortunately it wouldn't compile as ruby relies on libyaml, we need to add meta-oe from openembeded repository to satisfy dependencies.
    
    Finally my bblayers.conf looked like this:
    
    <script src="https://gist.github.com/misza222/9348068.js"></script>
    
  3. Compiling package
    
    `bitbake ruby` compiles your new package for target architecture.
  
  4. Customizing what goes onto the image (finally!!!)
    
    In a nutshell add `IMAGE_INSTALL_append = " ruby"` to the end of your conf/local.conf. For details see [yocto docs about extending image](http://www.yoctoproject.org/docs/1.6/dev-manual/dev-manual.html#usingpoky-extend-customimage).
    
  5. Build image as normal

