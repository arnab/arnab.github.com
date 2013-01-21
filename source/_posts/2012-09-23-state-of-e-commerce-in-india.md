---
author: Arnab
title: State of e-commerce in India
excerpt:
layout: post
categories:
  - on life
  - tech
tags:
  - ecommerce
post_format: [ ]
---
So, since moving back to India 4 months ago, we’ve trying to buy stuff
off the internet, like we did back in Seattle (oh Amazon), from
diapers to audio CDs (whaaaat? I know). While the world is much much
better compared to 2006, there are still some Idiocracies in the UX
and process. There are the big players ([FlipKart][1], [infibeam][2]
and the like) where (from the 4 months experience) you’d find what you
are looking almost 6-7 times out of 10. The long-tail of e-commerce in
India is the real deal though – the tail is really really long. I use
[Junglee.com][3] to find the long time and almost always (9+ out of
10) the things I am looking for are found somewhere. Funny thing is
that you’ll never find two things you need in one site. Over these 4
months, I don’t think any of these sites have come up more than once
in my search.

<!-- more -->

To highlight some of the other differences:

*   **No guest checkout**: Almost nobody has guest checkout. Everybody
      requires you to register and require your email and phone. Most
      the package tracking is done thru SMS so that’s ok, but I’ve had
      some spam (email and SMS) originating from here as well. But for
      the most part, they are well behaved (I don't know why they need
      my birthday or gender to ship stuff me though– anyway they get
      wrong info for such questions ;))
*   **Weak integration with backend**: More than once I have placed
      orders (after signing up etc.) only to be informed later that
      the item is not in stock. The websites are more like marketing
      websites with a cart/checkout process and it looks like the
      orders are processed completely separately.
*   **Cash-On-Delivery**: Almost everyone takes COD orders. I know
      some people don’t like the idea, but for Indian e-commerce it’s
      a must. Mostly because if you pay when you order on the site and
      then you don’t get the thing or get something else, there’s
      pretty much nothing you can do. Most sites will process a refund
      but you have to call them a few times to get that done. And some
      sites only give you a coupon that you can use in their site. So
      COD is heaven-sent and must-needed for such small sites.
      [FlipKart has started doing Card-On-Delivery][5], which is even better!
*   **Faaaaaast and FREE shipping**: Almost every order I have made
      has been delivered within a few days. In one-third of the cases it’s
      within 2 days. And it’s 99% of the time free shipping.

To summarize, for the most part, it’s all good. You can find 9/10
things online and of that you can get 9/10 items delivered at your
doorstep within a reasonable amount of time and pay after you
get/inspect it. But that’s not why I started writing this piece today…

## A uniquely horrible experience at ezmaal.com

What I wanted to do today was share a very bad experience on one of
these small player’s sites today. Remember the band called
[Silk Route][6]? Heard them on radio and remembered how awesome their
music was. Unfortunately the album’s not on spotify or in Amazon/MP3.
So I looked up FlipKart (out of stock) and Junglee. That’s where I
found [ezmaal.com][7] – and they had it in stock! So I went through
the registration process and signed up for an account.

Now, I use the [most excellent 1Password][8] for creating random
passwords for every site and to manage signing-in/out. Did the same on
ezmaal too – and it was all fine and dandy and got an account created.
Now, just before checking out I wanted to see if the login/logout was
working (you never know with small sites). So I opened up the site in
an [incognito window][9] and tried loggin in. Here’s the screenshot of
what I got back: [![ezmaal login failure][11]][11]
click to see larger image

1.  They throw a really garbage un-customized ASP.net error in the
customer’s face. It means nothing to me!
2.  They are trying to validate my password for script-injection. I
don’t think they are actively doing this, but it’s probably part of
ASP.net and they have not tested and not coded to handle login
failures. Really really bad if the login on your site throws up gibberish.
3.  **Password displayed on screen**: The worst part is that they
print my password three times on the screen, verbatim. Thank God I use
1Password and have a random (and more importantly, different) password
on every site. But like most customer’s if I had a
one-password-for-all and used that in here, it’s as good as being
leaked. If nowhere else, this will be on their server-logs. An
employee only need to grep for `Password\=` in the logs. On top of
this, with this kind of an experience, I have no faith that they
salt/hash the passwords. I am more willing to believe that they keep
it all in cleartext in a SQLServer database.

I have seen bad e-commerce sites before, but will I shop at a place
which does not care about my online security? No way in hell (yeah, I
did not complete that order)!

 [1]: http://www.flipkart.com/
 [2]: http://www.infibeam.com/
 [3]: http://www.junglee.com/
 [4]: http://www.arnab-deka.com/posts/wp-includes/images/smilies/icon_wink.gif
 [5]: http://www.flipkart.com/s/help/payments
 [6]: http://www.amazon.com/Route-Indian-Music-Hindi-Modern/dp/B0013LKL36/
 [7]: http://www.ezmaal.com/
 [8]: https://agilebits.com/onepassword
 [9]: http://support.google.com/chrome/bin/answer.py?hl=en&answer=95464
 []: http://imageshack.us/a/img710/4540/ezmaalloginfailure.png
