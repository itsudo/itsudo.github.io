---
layout: post
title:  "Create mongo indexes with mongoid and without rails"
date:   2013-10-14 21:01:21
categories: mongodb
---

In rails you have convenient rake tasks, but what if you are not using rails?

Just call `YourModel.create_indexes`. For details see [mongoid indexable module](https://github.com/mongoid/mongoid/blob/master/lib/mongoid/indexable.rb)
