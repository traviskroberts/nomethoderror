---
layout: post
title: "Using PhoneGap FileTransfer to Download Multiple Files to the Device"
date: 2013-11-17 18:46
comments: true
categories: [mobile, phonegap]
---

I've been working recently on a [PhoneGap](http://phonegap.com/) app that is designed to operate offline, and receives incremental data updates from an API when the user has an Internet connection. These incremental updates also include new/updated product images. Since the app needs to operate offline, I have to download the files to the device when they are updated or added so they can be shown offline.

PhoneGap has [File and FileTransfer](http://docs.phonegap.com/en/3.1.0/cordova_file_file.md.html) plugins that allow you to access the device's file system and even upload/download files. The problem with these plugin are, almost all of the actions trigger callbacks, so it's hard to keep the thread of what is happening. The PhoneGap documentation for these plugins are slightly lacking, so it was difficult to figure out how to accomplish what I needed. Through a lot of Googling and trial & error, I was finally able to get the following code working.

{% gist 9c8c9f1cc8d8d002dd5e image_download.js %}

Ok, we have the files downloaded, but how to we show them in our app. As far as I could find, you can't refence images on the device's filesystem form the PhoneGap app.

Luckily, the PhoneGap File plugin has a way to read files from the filesystem. It includes a method to read the file as a data url which converts it to a base64-encoded string.

My app was written using Backbone with Handlebars templates. So, to display the image, I wrote a Handlebars helper to get the image from the file system and return it as a base64-encoded string. You'll notice that the helper actually gets an element via jQuery and sets it `src` attribute. I had to do it this way since all of the File plugin methods are asynchronous and handled with callback.

{% gist 9c8c9f1cc8d8d002dd5e handlebars.js %}

The helper can be called like so:

{% gist 9c8c9f1cc8d8d002dd5e template.hbs %}
