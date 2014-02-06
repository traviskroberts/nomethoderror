---
layout: post
title: "ActiveRecord Random Ordering with Pagination"
date: 2014-02-05 21:18
comments: true
categories: [mysql, postgresql, activerecord, rails]
---

When I created [nshvll.org](http://nshvll.org/), I wanted the ability to show the user a randomly ordered list of members. I also wanted to paginate the results, and I didn't know if it was possible to have both. After a little research, I found that you can pass a seed to the mySQL `RAND()` function and have it return an identical list each time it's called.

## mySQL

Since I want each person to get a uniquely randomized list of members, I set a cookie with a seed which is randomly generated (1-100).

I set the seed in a `before_filter` in my `ApplicationController`.

{% gist 8838030 application_controller_mysql.rb %}

Notice, I only set the cookie if it doesn't exist. I also set the expiration of the cookie to 15 minutes because I don't want the user to get the same list of members *all* the time.

Now, in the `MembersController`, I can pass that seed to mySQL and get a repeatable sequence of random records.

{% gist 8838030 members_controller_mysql.rb %}

## PostgreSQL

A little while after I built the site, I decided to move it from a personal VPS to [Heroku](https://www.heroku.com/). To do that, I needed to convert the database to PostgreSQL (or pay for a mySQL option). After a little research, I found out that PostgreSQL is a bit trickier than mySQL when it comes to using a seed with the `random()` function. You have to run a separate select query to set the seed before the query that gets the list of records.

{% gist 8838030 members_controller_postgres.rb %}

PostgreSQL's `setseed()` function requires a number between -1 and 1, so we need to switch to a random float instead of an integer in the `ApplicationController`

{% gist 8838030 application_controller_postgres.rb %}

There we go. A repeatable, randomized set of records in mySQL or PostgreSQL.
