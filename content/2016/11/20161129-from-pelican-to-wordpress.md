+++
title = "Migrating from Pelican to Wordpress"
date = "2016-11-29"
slug = "from-pelican-to-wordpress"
+++

![Planning](/media/2016/riqyl8ivwek-evan-clark-2.jpeg "Planning")

I've migrated my [main blog](http://zoia.org) from Pelican to Wordpress. ([Pelican](http://blog.getpelican.com/) is a static blog generator.)

The main reason for changing is that I to make some changes in my webpage layout, or add some feature like a landing page, but don't want to make (program) all the changes myself.

Using Wordpress will add complexity to my publishing workflow, but things like implementing landing pages and writing custom page archives can be quickly done in Wordpress by using the appropriate plugin. Also, I don't have time to make sure my Pelican template/theme/skin stays responsive web-wise each time I need to change something.

My Pelican setup used a combination of Pelican, the program, installed on a Linode server, that generated my blog from a folder in the same server.  The folder was kept in sync with my laptop using Dropbox.  (More about this setup [here](http://code.zoia.org/2014/02/25/pelican-dropbox-automatic-blog-regeneration/).

## Every Rose has Its Thorne

Installing Wordpress from scratch in my Linode server, choosing a theme, and installing some basic plugins took around an hour.  The most time consuming step, however, was migrating the content to Wordpress.

### Markdown Issues

I've been writing my posts in Markdown for some years now. The idea is that I can take my content everywhere, because Markdown is close to an universal jargon, so to speak.  The idea is to "own" your content so you can take it with you to whatever blogging platform you use, and the content being as close to human writing as possible (which HTML is not).

In reality, however, the Markdown _flavor_ Pelican uses is not 100% compatible with the flavor Wordpress uses (I'm using the one provided with Jetpack).  The main difference is how you specify html attributes like classes to your markdown.

For example, my book reviews include a image of the book. It's format is specified using a `class="imagebook"` attribute, which in Pelican looks something like this:

~~~
![Deep Work](http://.../bookcover.jpg){: class="bookimage" }
~~~

In Wordpress' Markdown, the same line should look like this:

~~~
![Deep Work](http://.../bookcover.jpg){.bookimage}
~~~

Also, while I could add attributes like `{: target="_blank" }` to any link, Wordpress' Markdown doesn't provide (as far as I know) anything similar. (This is just a consequence of Markdown extensions not being standardized.)

My solution for this was simple:

Use a text editor ([Atom](https://atom.io/), in my case) and open the folder containing all my content.  Then, use Find/Replace project-wise to replace Pelican markup for Wordpress' flavor. (Forget about `{: target="_blank" }`, just settle down for external links to open in the same browser window.)

Lesson learned:

### Disqus Comments

The second pain was migrating [Disqus](https://disqus.com/) to Wordpress.

Disqus uses your Disqus shortcode (a sort of username) for identifying your account.  Then, it uses a unique identifier to identify the comment thread for each of your posts. This identifier is passed as the `disqus_identifier` variable in the Javascript code that actually load the comments on the web page.

In my Pelican setup, the unique identifiers for each post were created using the one thing that is unique for each post:  it's permalink, without the domain.  Like in `/2014/02/25/pelican-dropbox-automatic-blog-regeneration/`  My idea behind this was, again, to be able to take the comments with me to whatever blogging platform I choose.

Wordpress' Disqus plugin, however, has another idea of what constitutes a unique identifier. It uses Wordpress' unique post ID to build it:

~~~
1119 http://zoia.org/?p=1119
~~~

The problem is that the `1119` is unique to Wordpress, and there was no easy way to convert my existing Disqus IDs to that format.

My solution was to hack the Disqus' plugin code so that it generated the unique identifier in my own format:

~~~
function dsq_identifier_for_post($post) {
// return $post->ID . ' ' . $post->guid;
return rtrim(parse_url(get_permalink($post), PHP_URL_PATH),'/');
}
~~~

The problem: I'll need to patch the code every time the plugin is updated.  The benefit:  I keep my more logical (to me) identifier structure.

### Migrating content itself

I tried several plugins to import my content directly into Wordpress, without success. Pelican is not widely used, so there is no direct way to migrate your content to Wordpress.

Being my posts a bunch of text files with YAML headers residing in a folder on my laptop, at first I thought of writing a Python script that read every file, extracted the post's metadata from the YAML header, and injected it into Wordpress using the Wordpress API and an appropriate Python library. (Which there are plenty.)

For every post, I would have to check for links to local image files. If found, the image file would be uploaded to Wordpress, and its new URL would replace the original one in the post.

This is not a difficult script to write, but I'm sure it won't be without it's pitfalls.  And then, knowing myself, I would still want to check every post to see if it rendered OK.

So, I opted for a more manual procedure:  copy each post manually.  (Yes, I know what you are thinking...) I did this in 30 minutes chunks, for several days.  Not the fastest thing, but it did get the work done. The third day, I became tired of this manual procedure and wrote a Pelican exporter.  (You can download it from [Github](https://github.com/robertozoia/pelican-to-wordpress).)


## Template tweaking

I'm using Genesis as the base theme. I used the Genesis Sample Child theme as a base to customize my blog's appearance to mimic its previous incarnation. Almost 100% of this was done by adding to the CSS file.  Genesis is a good alternative, and not being a CSS specialist, it's structure is clear and relatively easy to adapt to your needs.

## Lessons learned

For me having my content in a format portable enough that allows me to republish it wherever I need is an important requirement.  Using Markdown is a good way to do it.  Actually migrating the content is not as simple as it sounds, however, but it can be done.








