---
layout: post
title: "ActiveAdmin: Custom MetaSearch Filter"
date: 2014-02-23 17:06
comments: true
categories: [rails, activeadmin]
---

Recently, I had the need to create a custom ActiveAdmin filter for a site I was working on. I couldn't find much information on the subject, but after digging around, it turns out that it's pretty easy.

Here are my (admittedly contrived) models. You can see that a User belongs to an Account and an Account belongs to a Group. For this example, let's say I want a filter in ActiveAdmin on the User resource that lists all the Groups.

{% gist fdae2afefe12dd888633 1_models.rb %}

Here's my simplified ActiveAdmin resource, with the added filter.

{% gist fdae2afefe12dd888633 2_user_resource.rb %}

To hook it up to the model, I just need to add a scope and a call to the built-in MetaSearch method `search_methods`.

{% gist fdae2afefe12dd888633 3_user_model.rb %}
