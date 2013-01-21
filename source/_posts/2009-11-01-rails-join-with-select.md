---
author: Arnab
title: Rails - Table join with specified fields in select
layout: post
category: programming
tags:
  - active_record
  - programming
  - ruby
  - rubyonrails
  - sql
---
Figured this out after a lot of monkeying-around (I mean `script/console`).

Situation:

+ I have two tables (Revisions `has_many` Inputs)
+ I can load Revisions and then for each I can find Inputs, but quickly found out that for my situation, it leads to a lot of queries. So I want to load the required fields from both tables together

`:joins` is the only way to do this, using `:includes` does __NOT__ respect the select clause. Here a gist:
{%gist 223925 %}

Admittedly, this is hacky, too hacky for my comfort. Comment/suggest a better/cleaner solution?

Note: Found out that there is a gem to do this: [ar-select-with-include][1]

 [1]: http://code.google.com/p/ar-select-with-include/