---
layout: post
title: "Track Backbone.js Page Views with Google Analytics"
date: 2013-11-19 19:42
comments: true
categories:
---

Google Analytics tracks page views based on evaluating the tracking code on page load. Backbone.js makes this difficult because the page never reloads. Fortunately, it's super easy to add a function to the Backbone router to manually track each route.

## Newer Analytics Code

If your tracking code looks like below, then you have the newer Analytics tracking code that uses the `ga` function instead of the `_gaq` array.

{% gist 9d05cb3d9c6d90408325 analytics_new.js %}

Add the following code to your router:

{% gist 9d05cb3d9c6d90408325 router_new.js %}

## Old Analytics Code

If your tracking code looks like this:

{% gist 9d05cb3d9c6d90408325 analytics_old.js %}

Add the following code to your router:

{% gist 9d05cb3d9c6d90408325 router_old.js %}
