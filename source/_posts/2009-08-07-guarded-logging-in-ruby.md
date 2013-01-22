---
author: Arnab
title: Guarded logging in Ruby?
excerpt: talking about and simple-benchmarking "guarded logging", a Java best practice in Ruby's context.
layout: post
category: programming
tags:
  - benchmarking
  - best-practices
  - java
  - performance
  - programming
  - ruby
---
Assuming you know about “guarded logging”, a Java logging best
practise. If not, get an overview in [this IBM article][1] or in [this blog][2].

Basically it is the practice of checking if a particular log message
will indeed be outputted to the log (based on the severity level)
before calling the log statement. This is a performance improvement.
Here's a Java example:
{% gist 4585349 example.java %}

So I heard from one of my colleagues that Ruby's logging performance
can also be improved the same way, by putting the message in a block
(instead of just passing it as an string arg to the method):
{% gist 4585349 example.rb %}

See various ways to log a message at the [ruby-docs][3] (search for
"How to log a message" in that page). I looked into the source-code
and, just like in Java, the first thing that is done is to check the
severity and return (true) if the severity is higher than the
message's. So like in Java, it should not have any effect (except
creating the strings etc.).

Just to test it out, I wrote a benchmark test:
{% gist 4585349 benchmarking_example.rb %}

Here's what I noticed:

* with `n <= 10,000` (number of logging calls), there was really no
  difference between the three ways:
  {% gist 4585349 results_small_n.sh  %}

* with `n = 100,000`: It looked like the simplest way to log (with a
  string-arg) still performs the best:
  {% gist 4585349 results_medium_n.sh  %}

Final takeaway: it really does not make that big a difference and
keeping it simple (with a string-arg) should work. If you are worried
about performance, this probably is not a trick that will give you a
big bang for the buck.

 [1]: http://publib.boulder.ibm.com/infocenter/ledoc/v6r11/index.jsp?topic=/com.ibm.rcp.tools.doc.appdev/serviceability_java.util.loggingbestpractices.html
 [2]: http://www.burlesontech.com/wiki/display/btg/Java+Logging+Standards+and+Guidelines
 [3]: http://www.ruby-doc.org/stdlib/libdoc/logger/rdoc/
