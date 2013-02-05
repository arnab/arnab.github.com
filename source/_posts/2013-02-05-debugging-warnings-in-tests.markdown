---
layout: post
title: "Debugging warnings in tests"
date: 2013-02-05 14:28
comments: true
categories: ruby,rails,test-unit,testing,debugging,obsecure
---
```sh
Object#id will be deprecated; use Object#object_id
```
Hate seeing warnings in your test output? Yeah me too. Came across a
fairly weird bug today and this is how I debugged it.

<!--more-->

With a recent checkin I started seeing some warnings in the test
output, like this:
```sh
$ ruby -I "lib:test" path/to/example_controller_test.rb
Loaded suite example_controller_test.rb [app_name] init ...
Started
........../path/to/some/_partial.html.erb:48: warning: Object#id will
be deprecated; use Object#object_id
.............../path/to/some/_partial.html.erb:48: warning: Object#id
will be deprecated; use Object#object_id
..........................................................................................
Finished in 12.545861 seconds.

 58 tests, 198 assertions, 0 failures, 0 errors
```

If life's easy, you'll see the test files name along with the
warnings. However, in this case, the trace only contains an erb
partial. The partial looked something like this:

```html
<li>
  <%= @something.try(:id) %>
</li>
```

Typically this warning happens when you call `#id` on an object that
evaluates to `nil`. In this case, looks like someone already thought
of that - and used
[`#try`](http://api.rubyonrails.org/classes/Object.html#method-i-try)
specifically to avoid this warning.

What gives? What complicates this is that our test suite has 1000+
tests and the partial that shows the erorr is used widely. (You could
try deleting the partial and see what fails but in this case 90% of
the tests would fail).

After some more trial and error, I started reading the Test::Unit
source on github. That with some introspection showed that you can get
the running test's name at runtime with the `#name` method. Duh!

So I added a `teardown` to the suite:
```rb
class ExampleControllerTest < Test::Unit
  # setup etc.

  def teardown
    puts "#{name}\n"
  end

   test "something should do something" do
     get :new
     # assert something
   end

   # more tests
 end
```

With that, my test suit printed out the name of every test right after
the `.` - and looking through the output for the warning showed me the
test that was causing it:
```sh
/path/to/some/_partial.html.erb:48: warning: Object#id will be
deprecated; use Object#object_id
.test_something_should_do_something(ExampleControllerTest)
```

This gave me the lead I needed. Now it took some more debugging to
figure out the details (I'll spare you the rest) but it turns out a
method 4-5 levels down was retruning `false` instead of `nil`. And
`#try` works beautifully for `nil` but not for `false`:

```rb
>> nil.try(:id)
=> nil
>> false.try(:id)
(irb):9: warning: Object#id will be deprecated; use Object#object_id
=> 0
>>
```

So there you go. It sure was an entertaining session for me. And if
you read it till here...

More techniques about how I could have debugged this more easily are
most welcome.
