---
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
title: "Allowing and testing CORS requests in Rails"
date: 2012-09-19 14:28
categories: ruby,rails,test-unit,testing,backbone,api,cors,http,service
comments: true
---
I’m currently writing a `backbone`-based `Javascript` app that’s going
to directly call a `REST`-style API (implemented with `Rails` ).

> CORS (Cross-Origin Resource Sharing) is new technique makes it
  possible for AJAX requests to directly talk to HTTP-services outside
  it’s own domain. Read this [awesome primer][1] to read more on CORS.


While there are lots of examples that show how to allow CORS requests
in Rails (just [google][2]), they almost never have tests with them.
While it’s simple to test the HTTP headers, you may have to look
around a little (or a lot) on how to test a HTTP “OPTIONS” request.
When you make CORS requests, the browser may make a pre-flight
“OPTIONS” request to verify that the server allows CORS.

<!-- more -->

To make Rails set the right HTTP headers to allow CORS requests, you
can do something like this:

```rb
# some_controller.rb

before_filter: allow_cors

def allow_cors
  headers["Access-Control-Allow-Origin"] = "*"
  headers["Access-Control-Allow-Methods"] = %w{GET POST PUT DELETE}.join(",")
  headers["Access-Control-Allow-Headers"] =
    %w{Origin Accept Content-Type X-Requested-With X-CSRF-Token}.join(",")

  head(:ok) if request.request_method == "OPTIONS"
  # or, render text: ''
  # if that's more your style
end
```

A few things to note here:

1. You can set the `Access-Control-Allow-Origin` header to your
domain to further restrict it.

1. While Rails is one place to do this in, you can certainly do this
in your webserver (nginx etc.). Again, just google. I prefer things to
be more testable – maybe when I see a performance problem, I’d revise
this decision (although, performance bottlenecks would probably not be
in setting HTTP headers).

Another thing to consider when you allow CORS, is authentication – you
should do some HTTP based auth (token auth for example) so only *your*
apps can talk to this service. The thing with JS is, however uglified
it is, any developer worth his salt can figure out how to call your
backend service after reading your JS by loading your site up in a
browser.

In any case, how do you test this? It’s fairly trivial to test that
the right HTTP headers were set with something like this:

```rb
# testing_cors_spec.rb
response.headers['Access-Control-Allow-Origin'].should == '*'
```

To make a HTTP `options` request in RSpec, I had to dig through some
code. And googling didn’t help here, at least the way I google. Here’s
the low-down: `RSpec` *delegates* the request methods (like
`get`/`post`/`put` etc. in the controller specs) to Rails’
`ActionController Tests`. All these methods invoke
`ActionController::TestCase#process` with specific args, one of which
is the method name.

Now, Rails master already has support for making
`options` requests in tests (thanks to [this commit][3]), but that’s
not available in the latest Rails release (3.2.8). I think this would
make it’s way into Rails 4.

Looking into this commit, we get the idea
though: basically we also call the `process` method with a `OPTIONS`
argument for the request-method. Putting it all together, my tests
looked something like this:

```rb
# some_controller_spec.rb

shared_examples_for "any request" do
  context "CORS requests" do
    it "should set the Access-Control-Allow-Origin header to allow CORS from anywhere" do
      response.headers['Access-Control-Allow-Origin'].should == '*'
    end

    it "should allow general HTTP methods thru CORS (GET/POST/PUT/DELETE)" do
      allowed_http_methods = response.header['Access-Control-Allow-Methods']
      %w{GET POST PUT DELETE}.each do |method|
        allowed_http_methods.should include(method)
      end
    end

    # etc etc
  end
end

describe "HTTP OPTIONS requests" do
  # With Rails 4 (currently in master) we'll be able to `options :index`
  before(:each) { process :index, nil, nil, nil, 'OPTIONS' }

  it_should_behave_like "any request"

  it "should be succesful" do
    response.should be_success
  end
end

# And similar tests for GET/POST what have you which actually test the functionality...
```

 [1]: http://www.nczonline.net/blog/2010/05/25/cross-domain-ajax-with-cross-origin-resource-sharing/ "Cross Domain AJAX with CORS"
 [2]: http://goo.gl/d8g3j
 [3]: https://github.com/rails/rails/commit/0303c2325fab253adf5e4a0b738cb469c048f008#L0R438
