---
layout: post
title: "ActiveAdmin: Redirect to Index on Create/Update"
date: 2014-03-10 21:46:18 -0500
comments: true
categories: [rails, activeadmin]
---

By default, [ActiveAdmin](http://activeadmin.info/) will display the `:show` action on create or update of a resource. Personally, I'd rather redirect to the `:index` action as long as the resource is valid.

You can overwrite ActiveAdmin's default behavior using the `controller` block.

{% gist 9478684 %}

Notice, I'm adding "if resource.valid?" to make sure we only redirect when there are no validation errors. If we didn't have that extra bit, the actions would **always** redirect to the `:index` action regardless.
