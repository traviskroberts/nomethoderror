---
layout: post
title: "Git Essentials - Hack &amp; Ship"
date: 2013-10-12 11:44
comments: true
categories: [git]
---

If you're like me, your normal git workflow looks something like this:

1. Do some work in a topic branch and need to rebase master into the branch.
2. `git checkout master`
3. `git pull origin master` (or `fetch` and `merge`)
4. `git checkout topic-branch`
5. `git rebase master`

Once you're done with your topic branch, it might look something like this:

1. `git checkout master`
2. `git merge topic-branch`
3. `git push origin master`

That's a lot of work, and as a developer we can definitely make that process easier. About 4 years ago, I came across a set of bash scripts that simplified this workflow greatly. The creator, [Rein Henrichs](http://reinh.com/), named them [Hack && Ship](http://reinh.com/blog/2008/08/27/hack-and-and-ship.html).

These tools worked great, but weren't flexible enough for me. They assumed that you would always be rebasing and pushing to the master branch. If this wasn't the case, you had to do everything by hand.

Here are my updated versions of Hack && Ship that allow you to rebase and push to any branch (such as `staging` or `qa`):

## Hack

{% gist 6952241 hack.sh %}

## Ship

{% gist 6952241 ship.sh %}

To use them, create two files named `hack` and `ship` somewhere in your path (like `/usr/local/bin` maybe) and make them executable. Then, you can invoke them like so:

`hack` or `hack staging`

`push` or `push qa`

`hack && ship`
