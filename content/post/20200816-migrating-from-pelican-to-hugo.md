+++
title = "Migrating from Pelican to Hugo"
date = "2020-08-16"
slug = "migrating-from-pelican-to-hugo"
tags = ["static-blogging", "hugo"]
+++

I've migrated this blog from [Pelican](https://getpelican.com/) to [Hugo](https://gohugo.io/).

This blog has always been a static/baked blog. Content is just a collection of html files which reside in a Linode instance.  This allows me to use a very minimal server instance to host it.  Dynamic content generators like [Wordpress](https://wordpress.org) generate content by extracting the articles from a database and producing a webpage on the fly, they allow for more complex setups, but also have a higher footprint.

The problem with Pelican is that once in a while, when I upgraded the software, my site configuration file broke. So instead of just publishing a new post, I had to spend time figuring out what had changed, testing the new configuration, etc. After evaluating some alternatives, I decided to give Hugo a try. It took me one morning to figure out Hugo, have a test site running on my laptop, move my posts to Hugo, and republish the blog on my server.

For the actual migration, I wrote a script in Python called [pelican-to-hugo](https://github.com/robertozoia/pelican-to-hugo) that collects all the Markdown files from my blog's  Pelican directory, and converts each post's header to Hugo's front matter in TOML format. You can modify the script to suit your needs.

Some issues with the migration:

* I broke my urls in the migration.  I previously used dates as part of the post's path (i.e., `https://code.zoia.org/2020/08/migrating-from-pelican-to-hugo/`), now I'm simply using `/posts/migrating-from-pelican-to-hugo/**.  I could write some code for the webserver to handle the redirection...

    **Update 2020-08-23**: Fixed the posts urls by duplicating the content under the original file structure.
* I fixed my internal image links by hand: searching in the post's directory for images, and changing the path.  I did this by hand instead of writting code to do it because I don't use that many images in my posts.

For know, I'm using a nice theme from [Djordje Atlialp](https://github.com/rhazdon/hugo-theme-hello-friend-ng) while I figure out how templates work in Hugo.
