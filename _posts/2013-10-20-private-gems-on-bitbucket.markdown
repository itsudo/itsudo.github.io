---
layout: post
title:  "Private ruby gems on bitbucket"
date:   2013-10-20 12:59:31
categories: gems
---

It is possible to host private gems securely on bitbucket.

It involves putting username and password in a Gemfile, so best create a new user and add it a read access to the repository with private gem.

Then just add this to the Gemfile:

    ...
    gem 'your-secret-gem', git: 'https://user-accessing-gem:its-password@bitbucket.org/user-hosting-gem/your-secret-gem.git'
    ...
    
and voila!

Same works with any other git hosting that allows you to access repos via https
