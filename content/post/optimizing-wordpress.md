+++
title = "Optimizing Wordpress on WPEngine"
author = ["Roberto Zoia"]
date = 2021-10-07
draft = false
weight = 1001
+++

Inspired by Kevin Quirk's post about [Core Web Vitals and Wordpress](<https://kevq.uk/core-web-vitals-and-wordpress/>), I spend some hours trying to improve the web vitals from my [other site](<https://zoia.org>), which runs on Wordpress. (You can measure your site's core vitals on [web.dev](<https://web.dev/measure/>).)

Some months ago I migrated that site from a self-hosted Linode instance to a managed solution on WPEngine. I'm essentially buying back time. A managed solution frees me from server admin duties, like making sure the latest Linux updates are installed, and PHP and its libraries up-to-date.

WPEngine offers an optimized Wordpress installation, which includes caching and CDN. Even so, the lighthouse test returned scores between 70-80 for both performance and best practices. While installing WP Super Cache gave me a near perfect score, WPEngine imposes some limitations on [what Wordpress plugins you can install](<https://wpengine.com/support/disallowed-plugins/>) and WP Super Cache in particular is not allowed.

After some hours of trying different plugins and comparing results, I finally settled for the following configuration:

-   Disable Jetpack's site boost and image optimizing. (Jetpack doesn't handle cache invalidation, so any image stored on their servers stays there forever... You'll need to upload the asset with a different name to use it again on your site.)
-   [Fast Velocity Minify](<https://wordpress.org/plugins/fast-velocity-minify/>) plugin for merging and minifying CSS and JavaScript, and compressing HTML.
-   [Lazy Load](<https://wordpress.org/plugins/rocket-lazy-load/>) by WP Rocket, for lazy-loading images _and_ videos without jQuery or other libraries.

Now the site gets substantially better [web vitals score](<https://lighthouse-dot-webdotdevsite.appspot.com//lh/html?url=https%3A%2F%2Fzoia.org>).

{{< figure src="/media/2021/zoia-org-web-vitals-2021-10-07.png" >}}

The perfectionist in me would aim for 99%-100% in all categories, but I don't think I can get there via plugins.  The next improvement should be reducing the site's footprint, which is currently around ~1MB uncompressed.
