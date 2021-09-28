---
layout: post
title:  "First real post of the new blog, done with Jekyll"
date:   2021-09-04 22:05:55 +0200
categories: software
---
I installed Jekyll on github.io following this YouTube tutorial (in german):
- Blog erstellen in unter 10 Minuten:
  [https://www.youtube.com/watch?v=BN02trD79aU](https://www.youtube.com/watch?v=BN02trD79aU)

I had quite some troube with my old MacOS Mojave:
- I needed to install a new version of Ruby (had 2.3 installed before), now 3.0.2.
- needed to put the new ruby to the path:

  `echo 'export PATH="/usr/local/opt/ruby/bin:/usr/local/lib/ruby/gems/3.0.0/bin:$PATH"' >> ~/.bash_profile`
- then install jekyll: `gem install bundler jekyll`
- needed to add a "forgotten" dependency manually:
  `bundle add webrick`

When modifying the "_config.yml" of the generated Jekyll website archive, make sure that you do not
use the "@" before your twitter name, or the website won't build. The error message was
also misleading.

