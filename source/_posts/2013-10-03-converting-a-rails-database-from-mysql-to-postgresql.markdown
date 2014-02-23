---
layout: post
title: "Converting a Rails Database from mySQL to PostgreSQL"
date: 2013-10-03 18:18
comments: true
categories: [rails, mysql, postgresql]
---

The [taps](https://github.com/ricardochimal/taps) gem allows you to transfer database structure and data easily between db types.

## Add the necessary gems to your Gemfile

{% gist 6818918 1_gemfile.rb %}

Make sure you have the gems for both db types you'll be accessing.

{% gist 6818918 2_gemfile.rb %}

## Start the taps server

This will connect to the database that you are copying structure/date *from*.

{% gist 6818918 3_taps.sh %}

`authusername` and `authpassword` can be whatever you want. This will be used to authenticate when pulling from this db server.

## Pull the data into your new database

Make sure the new database has been created.

{% gist 6818918 4_taps.sh %}

Done!
