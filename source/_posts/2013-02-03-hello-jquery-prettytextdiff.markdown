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

<iframe class="jsfiddle"
        style="height: 430px"
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
```js
diff_match_patch.prototype.diff_prettyHtml = function(diffs) {
    var html = [];
    var pattern_amp = /&/g;
    var pattern_lt = /</g;
    var pattern_gt = />/g;
    var pattern_para = /\n/g;
    for (var x = 0; x < diffs.length; x++) {
      var op = diffs[x][0];    // Operation (insert, delete, equal)
      var data = diffs[x][1];  // Text of change.
      //var text = data.replace(pattern_amp, '&amp;').replace(pattern_lt, '&lt;')
      //    .replace(pattern_gt, '&gt;').replace(pattern_para, '&para;<br>');
      var text = data.replace(pattern_amp, '&amp;').replace(pattern_lt, '&lt;')
          .replace(pattern_gt, '&gt;').replace(pattern_para, '<br>');
      switch (op) {
        case DIFF_INSERT:
          html[x] = '<ins style="background:#e6ffe6;">' + text + '</ins>';
          break;
        case DIFF_DELETE:
          html[x] = '<del style="background:#ffe6e6;">' + text + '</del>';
          break;
        case DIFF_EQUAL:
          html[x] = '<span>' + text + '</span>';
          break;
      }
    }
    return html.join('');
  };
```

So I wrote a library to wrap around it - so the client doesn't have to
repeat this wherever they need to use it. You can find more on
[github](https://github.com/arnab/jQuery.PrettyTextDiff/) and it can
be downloaded from the
[jQuery plugins site](http://plugins.jquery.com/pretty-text-diff/).

Now, with this library you'd have to write just a couple of lines to
produce a beautiful looking diff, like this:
```js
$(selector).prettyTextDiff({
  // options
});
```

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
