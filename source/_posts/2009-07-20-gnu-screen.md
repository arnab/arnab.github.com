---
author: Arnab
title: GNU Screen
excerpt: >
  few words about the what, why and how of
  GNU Screen, a program that helps a lot
  with my productivity.
layout: post
category: tech
tags:
  - configuration
  - gnu
  - linux
  - productivity
  - tools
post_format: [ ]
---
If you have nothing to do with Linux you probably can stop reading now. Unless you want to get introduced to a very nice tool in the Linux world. I can say without doubt that this saves me at least an hour every month. In addition it gets you away from doing some mundane “set-up” like things every time to start working. It has a load of features but today I’ll just scratch the surface. But it’ll be enough to start you off and I promise you’ll be glad you found screen.

One of the programs that I love and can’t go through the day without is [GNU Screen][1]. It’s like a Window manager, but only for your terminals. You know, like you are working with so many terminals/consoles/terminal-windows all the time (one to the DB, one with vim open, one to run the tests, one to run the program etc., one to watch the logs, a few to prod boxes etc.). And then you disconnect and then reconnect (from home, somewhere else) and you have to set-up all that again?

Yeah screen can help you with all that. My work pattern involves connecting to a screen session (and I get all the windows/context loaded). Whether I connect from work, home from somewhere else, all I have to say is:

    $ screen -ls (to see what sessions I have running)
    $ screen -R some-session-name


And it’s wicked-easy to switch between different windows, search through your history etc. You can also configure it to do a few “start-up” things every time. For example, at home, I have screen

1.  configured to Open 4 windows when it starts up and
2.  have window-0 go to my code dir (to teh root of my [RubyOnRails][2] part of the site)
3.  start up [auto-test][3] on window-1
4.  show the logs on window-2
5.  ssh into the [blue host][4] (which hosts my site)

Since the windows are persisted, I don’t have to do all these things every time I connect (for a lazy programmer (and all programmers are lazy aren’t they?) that’s a lot of help). You can even share the screens with someone else (I have not tried that yet though).

Anyway, I hope you are sold by now. Even if you are not, spend some time (shouldn’t be more than a couple of hours) installing/configuring/running screen and you will soon reap the rewards. To get you started:

*   The GNU Screen home-page: [http://www.gnu.org/software/screen][1]
*   A good guide to installing/setting-up/using: <http://magazine.redhat.com/2007/09/27/a-guide-to-gnu-screen>
*   Once you start liking it you’ll need a cheat-sheet: <http://aperiodic.net/screen/quick_reference?do=show>

A word about configuring: heard that Ubuntu will soon shipping with decent .screenrc (sane default configuration) so you don’t have to. Meanwhile you can configure it yourself (as in the Red Hat guide above) or look at these cool options: <http://linux.dsplabs.com.au/gnu-screen-screenrc-configuration-file-p13/>. Here is my .screenrc:

    vbell off
    vbell_msg "Ring"

    # detach on hangup
    autodetach on

    # don&#039;t display copyright page
    startup_message off

    # scroll back
    defscrollback 1000

    # setup the caption
    hardstatus alwayslastline "%{-b gk}%-w%{+b kg}%50>%n %t%{-b gk}%+w %=%C%< "

    # right/left bindings
    bindkey "^[[c" next
    bindkey "^[[d" prev
    bindkey "^[[b" focus

    # Set the altscreen so that when you quit vi, it will go back to
    # what it was before
    altscreen on


And finally, my delicious links for screen. </p>
Happy “screen”-ing ![:)][6]

 [1]: http://www.gnu.org/software/screen/
 [2]: http://rubyonrails.org/
 [3]: http://nubyonrails.com/articles/autotest-rails
 [4]: http://www.bluehost.com/
 []: http://delicious.com/arnab.deka/screen
 [6]: http://www.arnab-deka.com/posts/wp-includes/images/smilies/icon_smile.gif