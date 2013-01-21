---
author: Arnab
title: Installing GLPK on a Mac
layout: post
category: programming
tags:
  - gnu
  - install
  - linear-programming
  - linux
  - mac
  - maths
  - open-source
  - optimization
---
## Obsolation note:

Thanks to [Dave Coleman’s comment][1] I found out that glpk is available through homebrew now! So you just need these 2 steps to get glpk now:

1.  [homebrew][2]
1.  `brew install glpk`

If you still want to read on, the old way is still here…

So you want copy-paste instructions to install [GLPK][3] on your Macbook? Here are the steps:

1.  Download the latest version of GLPK from <http://www.gnu.org/software/glpk/#downloading>
2.  *Optional:* Follow the instructions to verify the download (you might need to get GNU Privacy Guard or gpg for this. You can get it at <http://gnupg.org>)
3.  Say it’s downloaded to your “Downloads” directory, go there and execute the following commands (using the terminal)
        cd ~/Downloads
        tar -xzf glpk-4.43.tar.gz
        ./configure --prefix=/usr/local # see note [1]
        make
        sudo make install


4.  At this point, you should have GLPK installed. Verify it:
        which glpsol
        /usr/local/bin/glpsol


5.  … and try help:
        glpsol --help


Now that you are all set-up, read up this excellent introduction using GLPK: <http://www.ibm.com/developerworks/linux/library/l-glpk1>

Notes:

+ HiveLogic article on [why using /usr/local is better][4]
+ If you want MySQL support (or something “extra”) check out the INSTALL file in the package

 [1]: #comment-2787
 [2]: http://mxcl.github.com/homebrew/ "homebrew"
 [3]: http://www.gnu.org/software/glpk
 [4]: http://hivelogic.com/articles/using_usr_local