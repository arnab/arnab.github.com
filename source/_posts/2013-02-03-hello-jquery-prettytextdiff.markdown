---
layout: post
title: "Hello jQuery.PrettyTextDiff"
date: 2013-02-03 10:56
comments: true
categories: tech javascript jquery nlp text diff
---
For some work I did recently, I had to produce a visual diff of text.
A visual diff makes it easy for the user to understand what exactly
changed with a quick scan.

There's an excellent library from Google, called
[diff_match_patch](http://code.google.com/p/google-diff-match-patch/)
that does a really good job of analyzing the text and producing the
diffs in a programatic manner. However, it lacks the sauce to visually
present it to the user.

So I wrote a jQuery library which is a wrapper around Google's library
and makes it trivial to wow your users.

<!-- more -->

First, a demo (the fiddle can be found
[here](http://jsfiddle.net/arnab/YwSVY/)):

<iframe
        style="width: 100%; height: 430px"
        src="http://jsfiddle.net/arnab/YwSVY/embedded/result,html,js,resources,css/"
        allowfullscreen="allowfullscreen"
        frameborder="0">
</iframe>

While Google's library is excellent from a NLP-perspective, it does
not provide a way to show the diff in a beautiful manner. They have a
reference implementation to produce the diff in HTML, but recommend
you write your own (also this implmentation is inflexible in terms of
changing style/elements etc.).

Also, this library is produced in 7 different languages - so the code
that uses this is not particularly pleasing to look at.

Here's an example of the code you would have to write to produce a
good looking diff:
{% gist 4700669 pretty-diff.js %}

So I wrote a library to wrap around it - so the client doesn't have to
repeat this wherever they need to use it. You can find more on
[github](https://github.com/arnab/jQuery.PrettyTextDiff/) and it can
be downloaded from the
[jQuery plugins site](http://plugins.jquery.com/pretty-text-diff/).

Now, with this library you'd have to write just a couple of lines to
produce a beautiful looking diff, like this:
{% gist 4700669 pretty-diff-with-textdiff-plugin.js %}

Peek inside the fiddle demo to see more. You can also customize many
of the options - check out the documentation in the github repo.

Hope you enjoy it!

PS: Some of the motivation was also to flex my muscles with
CofeeScript (haven't had a chance to use it for the last 2-3 months)
and setting up compile and uglifying/compressing  of the Javascript
with `cake`. Check out the simple
[coffeescript code](https://github.com/arnab/jQuery.PrettyTextDiff/blob/master/jquery.pretty-text-diff.coffee)
and the
[Cakefile](https://github.com/arnab/jQuery.PrettyTextDiff/blob/master/Cakefile).

### Links

+ [Google's diff_match_patch library](http://code.google.com/p/google-diff-match-patch/)
+ [Plugin source on github](https://github.com/arnab/jQuery.PrettyTextDiff/)
+ [jQuery plugins site](http://plugins.jquery.com/pretty-text-diff/)
+ [jsFiddle demo](http://jsfiddle.net/arnab/YwSVY/)
