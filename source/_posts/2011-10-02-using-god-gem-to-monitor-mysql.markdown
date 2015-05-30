---
layout: post
title: "Using God Gem to Monitor mySQL"
date: 2011-10-02 12:00:00 -0500
comments: true
categories: [rails, mysql]
---

I recently ran into a problem on a client server where the `msyqld` process died, and neither of us noticed it for almost 24 hours. That meant that the site was completely useless that entire time. Needless to say, the client wasn't thrilled about this.

I told him that I'd look into setting up a monitoring service to, at the very least, notify me if `msyqld` ever crashed. During my research, I stumbled upon the god gem (which I'd used in the past to monitor mongrel processes back in the days before Passenger). I didn't realize it could be used to monitor other processes as well, such as `msyqld`.

God is a rubygem, so it's easy to install on any *nix operating system. It's config files are also written in Ruby, so that makes it even better.

What you'll need to get the script running:

1.  Install the god gem (as root).

    <pre>sudo gem install god</pre>

2.  Find the location of your `msyqld` pid file.

    <pre>mysqladmin -u root -p variables | grep pid_file</pre>

3.  Determine the command to start/stop/restart the `msyqld` service. Usually `/etc/init.d/mysqld`

Here is the config file I wrote to watch my mysqld process:

{% gist c1f96cfc74a73316c35b mysql.rb %}

A few things to note about my script:

1.  In my start and restart commands, I also restart Apache. Running my site with Passenger, I would get a Rack error when `mysqld` restarted, but apache hadn't. YMMV.
2.  I'm using an SMTP server for my email notification. You can also use `sendmail`, or you can exclude the email notifications altogether.
3.  When running the script for the first time, it's a good idea to add the `-D` flag. This runs god in non-daemonized mode so all output is piped to STDOUT. That way, you can watch what it's doing to ensure everything is working correctly.

For more information about the god gem, see their site: [god.rubyforge.org](http://god.rubyforge.org/)
