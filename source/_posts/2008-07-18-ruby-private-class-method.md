---
author: Arnab
title: Ruby private class method
excerpt:
layout: post
category: programming
tags:
  - ruby
post_format: [ ]
---
> The following is just so I can remember it… You need not read all this.

In Java, if you need a class whose constructor is private – so you can’t instantiate it from anywhere else, you’d do:

    public class AClass {
      private int a;
      private AClass(int a){
        super();
        this.a = a;
      }


In Ruby, it’s a bit different. The why will come later (dynamic language), but just hiding the initialize method is not enough. You can still create an object coz you are actually calling the new method:

    irb(main):001:0> class AClass
    irb(main):002:1>   attr_reader :a
    irb(main):003:1>   private
    irb(main):004:1>   def initialize(a)
    irb(main):005:2>     @a = a
    irb(main):006:2>     end
    irb(main):007:1>   def some_other_method
    irb(main):008:2>     "ha"
    irb(main):009:2>     end
    irb(main):010:1>   end
    => nil
    irb(main):011:0> obj = AClass.new(100)
    => #<aclass :0xb75768c4 @a=100>
    irb(main):012:0> obj.a
    => 100
    irb(main):013:0> obj.some_other_method
    NoMethodError: private method `some_other_method&#039; called for #</aclass><aclass :0xb75768c4 @a=100>
            from (irb):13
            from :0
    irb(main):014:0>


You’d have to hide the new method:

    class AClass
      attr_reader :a
      def initialize(a)
        @a = a
      end
      def self.test
        "test"
      end
      private_class_method :test
    end

    puts AClass.test


That shows:

    test.rb:12: private method `test&#039; called for AClass:Class (NoMethodError)


</aclass>