---
layout: post
title: "Shoulda Matcher Model Extras"
date: 2013-02-20 18:00
comments: true
categories: [rails, rspec]
---

If you use RSpec with your Rails projects, chances are you also use [shoulda_matchers](https://github.com/thoughtbot/shoulda-matchers) (and if you don't, what are you doing with your life?!). You probably already know all about the basic model matchers, like the ones below.

{% gist a3cb3677eb764b5cd365 1_user.rb %}

{% gist a3cb3677eb764b5cd365 2_user_spec.rb %}

### Association Extras

There are a ton of extra options you can use with the association matchers (pretty much any option you can pass to an association). Below are just a few.

{% gist a3cb3677eb764b5cd365 3_user.rb %}

{% gist a3cb3677eb764b5cd365 4_user_spec.rb %}

### Validation Extras

There are even more options for use with the validation matchers. Here's a small sampling (including some mass assignment matchers).

{% gist a3cb3677eb764b5cd365 5_user.rb %}

{% gist a3cb3677eb764b5cd365 6_user_spec.rb %}

These are just a few of the extras that <kbd>shoulda_matchers</kbd> offers. I would highly recommend that you read through the [documentation](http://rubydoc.info/github/thoughtbot/shoulda-matchers/master/frames) to discover all the things you can do.
