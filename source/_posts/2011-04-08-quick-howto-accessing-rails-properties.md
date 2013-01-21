---
author: Arnab
title: Quick howto on accessing Rails Properties
layout: post
categories: [programming, tech]
tags:
  - ruby
  - rubyonrails
post_format: [ ]
---
When you create a new Rails app the default static page (public/index.html) page shows a lot of details about the app. Here’s a quick how-to show these details (the idea is to probably show these on a /ping route (or a debug parameter on any page maybe) – so you can quickly monitor your app – it’s state, active_record state etc.).

<!-- more -->

**Rails 3**: browse the [source-code at railties/lib/rails/info.rb][1]

Or see:
{% gist 911091 rails_306_properties.rb %}

**Rails 2**: browse the [source-code at railties/builtin/rails_info/rails/info.rb][2]

Or see:
{% gist 911091 rails_202_properties.rb %}

Till the next time…

 [1]: https://github.com/rails/rails/blob/v3.0.6/railties/lib/rails/info.rb
 [2]: https://github.com/rails/rails/blob/v2.0.2/railties/builtin/rails_info/rails/info.rb