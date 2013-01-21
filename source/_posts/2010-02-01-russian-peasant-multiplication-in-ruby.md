---
author: Arnab
title: Russian Peasant Multiplication in Ruby
excerpt: >
  Simple implementation of Russian Peasant
  Multiplication in Ruby
layout: post
category: programming
tags:
  - github
  - maths
  - ruby
post_format: [ ]
---
Russian Peasant Multiplication: a very simple and elegant way to multiple.

Read more: [School-boy example of how and why it works][1] and about [Ancient Egyptian Multiplication on wikipedia][2]

So here’s my simple implementation: (or as a [gist on github][3])

    module RussianPeasantMultiplication
      def russian_peasant_multiply(b)
        numbers_to_add = []
        a, b = [self, b].sort #So we have the smaller number as the first

        negative_operands = [a, b].select { |n| n < 0 }
        result_should_be_negative = negative_operands.size.odd? # or negative_operands.size == 1

        # Now get the absoultes
        a, b = [a, b].map { |n| n.abs }

        while( a > 1 )
          a = a >> 1 # halv it
          b = b < < 1 # double it
          if a.odd? # or (a % 2 == 0 )
            numbers_to_add << b
          else
          end
        end
        result = numbers_to_add.inject(0) { |sum, n| sum += n }
        result = result * -1 if result_should_be_negative
        result
      end
    end

    class Integer
      include RussianPeasantMultiplication
    end

    # Tests
    require "test/unit"

    class TestInteger < Test::Unit::TestCase
      def test_russian_peasant_multiply
        assert_equal(22 * 70, 22.russian_peasant_multiply(70))
      end

      def test_russian_peasant_multiply_for_negative_numbers
        assert_equal(-22 * 70, -22.russian_peasant_multiply(70))
      end

      def test_russian_peasant_multiply_for_negative_arguments
        assert_equal(22 * -70, 22.russian_peasant_multiply(-70))
      end

      def test_russian_peasant_multiply_for_negative_numbers_and_arguments
        assert_equal(-22 * -70, -22.russian_peasant_multiply(-70))
      end

      def test_russian_peasant_multiply_for_zero
        assert_equal(0 * -70, 0.russian_peasant_multiply(-70))
      end

      def test_russian_peasant_multiply_for_zero_arguments
        assert_equal(-22 * 0, -22.russian_peasant_multiply(0))
      end

      def test_russian_peasant_multiply_for_zero_numbers_and_arguments
        assert_equal(0 * 0, 0.russian_peasant_multiply(0))
      end
    end

 [1]: http://mathforum.org/dr.math/faq/faq.peasant.html
 [2]: http://en.wikipedia.org/wiki/Ancient_Egyptian_multiplication
 [3]: http://gist.github.com/290219