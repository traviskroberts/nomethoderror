---
layout: post
title: "Simple Rails Form Honeypot"
date: 2014-02-26 20:48:48 -0600
comments: true
categories: [rails]
---

If you have a form on your Rails site, chances are you get a fair amount of spam submissions from automated bots. One solution for preventing spam is by using a captcha field. They usually work very well to prevent spam, but they add a burden to human users. Another, less intrusive solution is to use a honeypot. A honeypot is a field that only bots can see, so you can know a form submission is spam if that field has a value.

There are gems available that will add a honeypot for you, but if you prefer to implement it yourself, it's very straightforward.

In your form, just add an extra field that you'll use to detect unauthorized submissions. Make sure to name it something normal so spam bots will populate it. I prefer to use the name "content". Notice that the field has its tabindex attribute set to -1. This will prevent the field from being selected if a user tabs through the field. I've also added some inline hint text in case a user with a screen reader fills out the form.

{% gist 9201887 1_form.erb %}

In your stylesheet, just add some styles to make sure that a human won't see the field on a desktop or mobile device.

{% gist 9201887 2_styles.scss %}

The final step is to add a check in your controller to only process the form if the value of the field is blank. For me, I'm only sending a notification email if the form submission is certified anti-spam.

{% gist 9201887 3_controller.rb %}
