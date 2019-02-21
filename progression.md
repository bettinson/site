---
layout: post
title: Progression
permalink: /progression/
---

Progression is a minimal progress bar written in ruby. 

* [Github](https://github.com/bettinson/progression)
* [RubyGems](https://rubygems.org/gems/mb-progression)

It can be used like so:

```ruby
p = Progression.new(cats.size)

puts 'Updating cats'

cats.each do |c|
  c.cute = true
  p.tick
end

```

Which will output a simple progress bar:

```
Updating cats
========================================================
```

You can install it by adding this line to your application's Gemfile:

```ruby
gem 'progression'
```

And then execute:

```
$ bundle
```

Or install it yourself as:

```
$ gem install progression
```
