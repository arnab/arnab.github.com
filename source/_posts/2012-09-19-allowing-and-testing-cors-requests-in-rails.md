---
author: Arnab
title: >
  Allowing and testing CORS requests in
  Rails
excerpt:
layout: post
category: programming
tags:
  - api
  - backbone
  - cors
  - http
  - requests
  - rspec
  - ruby
  - rubyonrails
  - service
  - testing
post_format: [ ]
---
I’m currently writing a `backbone`-based `Javascript` app that’s going to directly call a `REST`-style API (implemented with `Rails` ).

> CORS (Cross-Origin Resource Sharing) is new technique makes it possible for AJAX requests to directly talk to HTTP-services outside it’s own domain. Read this [awesome primer][1] to read more on CORS.

While there are lots of examples that show how to allow CORS requests in Rails (just [google][2]), they almost never have tests with them. While it’s simple to test the HTTP headers, you may have to look around a little (or a lot) on how to test a HTTP “OPTIONS” request. When you make CORS requests, the browser may make a pre-flight “OPTIONS” request to verify that the server allows CORS.

<!-- more -->

To make Rails set the right HTTP headers to allow CORS requests, you can do something like this:
{% gist 3749227 controller.rb %}

A few things to note here:

1.  You can set the `Access-Control-Allow-Origin` header to your domain to further restrict it.
2.  While Rails is one place to do this in, you can certainly do this in your webserver (nginx etc.). Again, just google. I prefer things to be more testable – maybe when I see a performance problem, I’d revise this decision (although, performance bottlenecks would probably not be in setting HTTP headers.)

Another thing to consider when you allow CORS, is authentication – you should do some HTTP based auth (token auth for example) so only *your* apps can talk to this service. The thing with JS is, however uglified it is, any developer worth his salt can figure out how to call your backend service after reading your JS by loading your site up in a browser.

In any case, how do you test this? It’s fairly trivial to test that the right HTTP headers were set with something like this:
{% gist 3749227 testing_cors_spec.rb  %}


To make a HTTP `options` request in RSpec, I had to dig through some code. And googling didn’t help here, at least the way I google. Here’s the low-down: RSpec *delegates* the request methods (like `get`/`post`/`put` etc. in the controller specs) to Rails’ `ActionController Tests`. All these methods invoke `ActionController::TestCase#process` with specific args, one of which is the method name. Now Rails master already has support for making “options” requests in tests (thanks to [this commit][3]), but that’s not available in the latest Rails release (3.2.8). I think this would make it’s way into Rails 4. Looking into this commit, we get the idea though: basically we also call the `process` method with a “OPTIONS” argument for the request-method. Putting it all together, my tests looked something like this:
{% gist 3749227 controller_spec.rb  %}

 [1]: http://www.nczonline.net/blog/2010/05/25/cross-domain-ajax-with-cross-origin-resource-sharing/ "Cross Domain AJAX with CORS"
 [2]: http://goo.gl/d8g3j
 [3]: https://github.com/rails/rails/commit/0303c2325fab253adf5e4a0b738cb469c048f008#L0R438