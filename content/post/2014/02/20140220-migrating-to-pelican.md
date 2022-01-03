+++
title = "Blog migrated to Pelican"
slug = "blog-migrated-to-pelican"
date = "2014-02-20"
tags = ["ristretto", "static blog generators", "baked blog", "python", "pelican"]
+++


A year ago I started developing a static blogging engine called [Ristretto](https://github.com/robertozoia/ristretto). It was written in Python, used markdown files as input, Jinja2 for templating, and generated static html files on my web server.  Some weeks later, [I migrated](http://code.zoia.org/2013/01/07/blogging-with-ristretto/) my main blog ([zoia.org](http://zoia.org)) and this blog from Wordpress to my new blogging platform.

Compared to writing in Wordpress, I enjoyed the new platform a lot. Over 2013 I kept adding functionality to Ristretto.  At one point midyear, I rewrote part of the engine so that it read posts from a Dropbox account instead of the local folder.  The engine, now running on the web server, generated the blog using the Dropbox API.  Now I could write and publish from anywhere I could use a text editor and access my Dropbox account.

But reading files through the Dropbox API was _slow_.  I had to implement some caching mechanism to speed things up.  Other improvements followed... I changed the posts header structure (the post metadata) from my custom format to the more standard YAML, so posts could be easily ported to other blogging platforms if needed. I had to write some code around the RSS generator I was using (<code>pyrss2gen</code>) so it correctly embedded image urls in the RSS feed.

### Spend your time writing, not tweaking your blogging platform

I've been happy blogging with Risttretto.  But instead of spending more time writing, I was frequently trying to improving the code.  And there were some shortcomings in the way I had implemented the engine that kept bothering me.

First, if a post contains images, the image files have to be uploaded manually to the web server.  And you will have to figure out in advance the url that the images will have _when the post is published_, because the engine does no conversion of the url. (This also means that the images will not show in the post if previewed locally.)

Second, because of the way Ristretto is designed, the template files reside on the server and are not updated via Dropbox[^ristretto-syncing]. Whenever I found a minor bug in my template, I usually fixed it directly on the server... but later forgot to sync the changes with my local copy.

[^ristretto-syncing]: Keep in mind that Ristretto reads the blog posts using the Dropbox API, not through a local Dropbox folder.

And regenerating my two blogs, which have not so many posts, was still _slow_.

So, after some thought, I decided to migrate to another static blogging engine.  Ristretto has been a nice experiment, but I want to spend more time writing articles, not rewriting yet-another-static-blog-generator.

### Migrating to Pelican
I chose [Pelican](http://docs.getpelican.com/) over Octopress or other engines like Nerve because I had read very positive reviews about the engine, and because It's written in Python.  I'm very comfortable deploying web apps in Python, and I wanted to minimize the time required to switch engines.

Dropbox synchronicity and the ability to write posts from anywhere was not negotiable. After some web research, I followed [Joe Hewitt's advice](http://joehewitt.com/2011/10/03/dropbox-is-my-publish-button) and created a separated Dropbox account for my blog, and then shared a folder in that account with my main Dropbox account. This shared folder is where posts, images, and template files resides, and where I write new posts.

I installed [watcher](https://github.com/gregghz/Watcher) to monitor the folder containing my posts, and launch Pelican to regenerate the blog any time a change is detected[^some-trouble-with-watcher].

[^some-trouble-with-watcher]: I had some trouble with Python paths and <code>watcher</code> because the way <code>publishconf.py</code> in Pelican added the current directory to the Python path.

Converting my templates to Pelican templates was straightforward, because both Ristretto and Pelican use Jinja2. Only some variable name changes were required.

Migrating to Pelican was _fast_.  Having my two blogs running on Pelican, including writing a small script in Python to migrate my old posts's header structure to Pelican's format, took me around four hours.






