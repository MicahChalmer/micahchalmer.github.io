---
date: 2013-01-30 10:23 PM EST
title: If You Make Web Sites, The World Kisses Your Butt
layout: post
---

I am still amazed by the amount of web hosting and related services that are available for free as of this writing.  I volunteer as the webmaster for the [Baltimore Playwrights Festival](http://www.baltplayfest.org/).  Just look at all the organizations that actively help me do this, all for free:

<!-- ~~fold~~ -->

The site is hosted on [DreamHost](http://www.dreamhost.com/), which isn't generally free but does give a [free basic shared hosting account](http://wiki.dreamhost.com/Non-profit_Discount) for tax-exempt non-profit organizations like ours.  I use that because we have more than 100 MB of media (mostly scripts of submitted plays) to serve up--otherwise I might have gone with [Heroku](http://www.heroku.com) instead, which offers a more modern cloud-based hosting experience, and they have a plan that's free for everyone as long as it's very small.  And you know quite well they're paying amazon to run your site for free!  (Can't blame them for shutting it down quickly when it's idle...)  Or if you don't like that, try [Google App Engine](https://appengine.google.com/), Or, for a site that's only public static content, I would go for [GitHub Pages](http://pages.github.com/).  I used that for my wedding web site last year.  Quickly served, handles as much load as you could hope to get, and costs nothing.

But visitors to the site won't be hitting it directly--they'll actually hit the CDN and reverse proxy [Cloudflare](http://www.cloudflare.com/), which provides its basic services for zero dollars.  That includes protection from attacks, local caching of content, and more if you enable it.

A visitor that goes to the site can sign up online for our mailing list, which gets delivered into their inbox (and not your spam folder--no small feat for automated mailing) and has a nice working unsubscribe link.  All provided by [MailChimp](http://www.mailchimp.com/), for free.

There's more available to me if I need it!  Domain names aren't free, but if my web host didn't come with its own DNS hosting (DreamHost does, but the other free ones I mentioned above don't) then [NameCheap](http://www.namecheap.com/) would [host my DNS for free](http://www.namecheap.com/products/freedns.aspx)--even for a domain I registered with elsewhere!

Yes, I understand the business model.  I'm getting all this for free because my needs are so small that the marginal cost, while not zero exactly, is so close to zero that it's negligible.  If I had something bigger I'd have to pay.  But it still shocks me that it's all so cheap that it works out this way.

I still wonder if it also reflects a bit of a bubble that will eventually burst.  For instance, the BPF also pays nothing for a Google Apps account for its email--but that's because I signed up for it before [Google stopped offering free accounts](http://googleenterprise.blogspot.ca/2012/12/changes-to-google-apps-for-businesses.html).  How long will we still have the free use of our grandfathered account?  They don't say.  Will CloudFlare or MailChimp eventually need to do the same thing?  I don't know.

What I do know is that right now is an amazing time.
