---
author: Arnab
title: 'Emacs: change fonts dynamically based on screen resolution'
excerpt:
layout: post
category: programming
tags:
  - apple
  - customization
  - display
  - emacs
  - font
  - resolution
  - retina
  - screen-resolution
  - thunderbolt
  - tweaks
post_format: [ ]
---
I regularly switch between a [Thunderbolt display][1] at home and the [Mac’s native retina display][2] when I’m in a coffee shop or the like.

It bugs me that I have to adjust emac’s font manually when I switch displays – started “re-using” emacs again last week. So I automated this today:
{% gist 3774147 %}

You can see all my emacs customizations in Github [arnab/emacs-starter-kit][3] repo, which is based on the excellent [ESK v2][4].

 [1]: http://www.apple.com/thunderbolt/
 [2]: http://www.apple.com/macbook-pro/features/
 [3]: https://github.com/arnab/emacs-starter-kit
 [4]: http://technomancy.us/153