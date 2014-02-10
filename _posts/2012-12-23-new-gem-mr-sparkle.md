---
date: 2012-12-23 11:00 AM EST
title: "New \"Mr. Sparkle\" Gem for an Auto-Reloading Rack Development Server"
layout: post
---

After reading a thread on auto-reloading ruby code for Sinatra/Rack apps on the nesta mailing list, I read through the ["magical reloading sparkles"](http://namelessjon.posterous.com/magical-reloading-sparkles) blog post that was mentioned, and realized there's no reason you need a bunch of project-specific code to use that approach.  But I couldn't find an easy-to-use package already written, so I wrote it myself.  The resulting new gem is called "[mr-sparkle](https://github.com/MicahChalmer/mr-sparkle)."

The full README is at [the GitHub page](https://github.com/MicahChalmer/mr-sparkle) but the short version is this:  install the gem with `gem install mr-sparkle` and then run `mr-sparkle` in the root of your project.  Your app will be served at localhost:8080.  It will auto-reload when a file changes (like rerun) but it won't stop l istening when it does so, and it only reloads your own code, so the result should be faster than shotgun or rerun.
