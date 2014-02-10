---
layout: post
date: 2012-12-16 11:30 PM EST
title: How I run Ruby 1.9.3 on DreamHost
---

This is what I am using to run ruby 1.9.3 on [DreamHost](http://www.dreamhost.com/) shared hosting, regardless of the fact that by default it's still stuck on 1.8.7. It's based based on [DreamHost's own instructions for running a Rails 3 app](http://wiki.dreamhost.com/Rails_3#Using_FastCGI), but with some improvements to isolate the DreamHost-specific parts and make it easier to figure out what's wrong if there are errors.  My application uses Sinatra rather than Rails, but I don't see any reason why a Rails 3 app wouldn't work with this as well.  As long as it's a [Rack](http://rack.github.com/) app that has a `config.ru` like one might use with `rackup`, and as long as it uses [Bundler](http://gembundler.com/), this setup should work. 

<!-- ~~fold~~ -->

My setup has the following differences from DreamHost's example:

   * Uses [rbenv](https://github.com/sstephenson/rbenv) and [ruby-build](https://github.com/sstephenson/ruby-build) rather than RVM--mostly because I like that it doesn't completely take over the shell
   * Redirects stderr of the dispatch.fcgi script to a file--this is useful if your ruby code fails to initially compile, since DreamHost won't put that output anywhere you can see it otherwise--all you'll see is a "500 internal server error" in your browser. (Your `error.log` file in your DreamHost `~/logs` folder will just say "Premature end of script headers: dispatch.fcgi.") This is useful for figuring out what is wrong with a setup like this, when the code ran fine and passed all its tests on your home machine. 
   * A small tweak to the `Rack::PathInfoRewriter` code--I found that if you delete the `SCRIPT_NAME` key from the Rack `env` object then some Rack middleware will crash. I set it to blank instead.

Before I get to the gory details, a word of warning: the code below is not what I'm actually running--I removed some extra stuff that is specific to my own app and wouldn't be relevant here.  I might have introduced some mistakes in trying to clean it up for the general public, and I haven't tested this version.  Comments or corrections are welcome (put them on the [GitHub gist](https://gist.github.com/4316253)).

All the files below should go in your project root directory, which should also be configured as your web directory in the DreamHost panel.  Usually that means if your site was `example.com` and your user was `sampleuser` then you'd be putting these files, along with your Rack app, into `/home/sampleuser/example.com`.

First off, the script that will do the initial setup.  Run these commands in an SSH session, after you `cd` to your project root directory:

<script src="https://gist.github.com/4316253.js?file=dreamhost_rbenv_setup.sh"></script>

Next, set up `dispatch.fcgi`.  I use a shell script for `dispatch.fcgi` that handles all the DreamHost-specific environment cleanup and then executes the ruby script `dispatch_fcgi.rb`, which is based on DreamHost's recommended `dispatch.fcgi`.  This allows me to keep the DreamHost bits out of my ruby code altogether.

<script src="https://gist.github.com/4316253.js?file=dispatch.fcgi"></script>
<script src="https://gist.github.com/4316253.js?file=dispatch_fcgi.rb"></script>

Don't forget to make your `dispatch.fcgi` world-executable but not world-writable by executing `chmod 755 dispatch.fcgi`.

The last part is to install the `.htaccess` file that will route all the requests through `dispatch.fcgi`.  This was taken verbatim from DreamHost's wiki page and is fairly uninteresting:

<script src="https://gist.github.com/4316253.js?file=.htaccess"></script>

A word on performance: DreamHost will kill your app when it becomes idle for a while, and the next request it gets after it gets killed has to wait for it to start up.  This startup penalty, for my app, was somewhere between seven and ten seconds.  Once the app was started up it took between 200 and 500 msec per request, which I deemed to be good enough.

