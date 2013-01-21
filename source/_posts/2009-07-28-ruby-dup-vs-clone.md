---
author: Arnab
title: Ruby dup vs clone
excerpt: "A bit about Ruby's clone and dup methods. They both create shallow copies, so what is the difference between them?"
layout: post
category: programming
tags:
  - programming
  - ruby
  - tech
---
> This was written way before [StackOverflow launched][1], and
> certainly much before it became popular. Those were the days when
> programmers had find out answers themselves ;)
> This has since been [asked and answered][2] on StackOverflow.

I have had this question about the difference between Ruby's `clone`
and `dup` method multiple times now. And I have always had this fuzzy
feeling that "they are almost the same thing". Today my colleague
asked it again and I decided to dig it out. Here's what
[Ruby API docs][1] say about them:

### `Object#clone`
> Produces a shallow copy of obj - the instance variables of obj are
> copied, but not the objects they reference. Copies the frozen and
> tainted state of obj.

### `Object#dup`
> Produces a shallow copy of obj—the instance variables of obj are
> copied, but not the objects they reference. dup copies the tainted
> state of obj. See also the discussion under Object#clone. In general,
> clone and dup may have different semantics in descendant classes.
> While clone is used to duplicate an object, including its internal
> state, dup typically uses the class of the descendant object to create
> the new instance.
>
> This method may have class-specific behavior. If so, that behavior
> will be documented under the #initialize_copy method of the class.

So in essence, both produce shallow-copies of the object. `clone`
copies the frozen __and__ tainted state while `dup` copies only the
tainted state. Even after reading that documentation twice, it's still
murky in my head (probably coz I have not had *a chance* to write code
to notice the frozen or tainted state specifically.)

Here's a gem from ruby-talk that Google brought up. So
[Matz says](3):

> `clone` copies everything; internal state, singleton methods, etc.
> `dup` copies object contents only (plus taintness status).

And so I wrote a bit of code to see it myself (and thus remember it).
Here's a very simple `Person` class:
{% gist 4585462 person.rb %}

Now we instantiate a `Person`, `p` and add a singleton method to it to say hi:
{% gist 4585462 person_say_hi.rb %}

See that it's all working:
{% gist 4585462 validate.rb %}

Now create a clone and a dup of it:
{% gist 4585462 clone_and_dup.rb %}

Both the clone and the dup have the same instance variables (which are
shallow-copies BTW), but only the clone has the singleton method
(`#say_hi`) in it:
{% gist 4585462 dup_vs_clone.rb %}

So that makes me feel that `#clone` has to do more work than `#dup`
does. Hence `#dup` might be more beneficial for performance compared to
`#clone` (unless you really need to use clone). Comments are welcome!

 [1]: http://www.joelonsoftware.com/items/2008/09/15.html
 [2]: http://stackoverflow.com/q/10183370/117750
 [3]: http://ruby-doc.org/core/classes/Object.html
