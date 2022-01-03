+++
title = "From Thunderbird to mu4e and back to Thunderbird"
author = ["Roberto Zoia"]
date = 2021-06-03
tags = ["emacs", "email", "mu4e", "mbsync"]
draft = false
weight = 1002
+++

I spent a couple of days configuring Emacs as an email client in my MacBook. There are lot of useful pages available on how to achieve this. The setup involves using a program like `mbsync` or `offlineimap` to create and maintain a local copy of your emails accounts on your computer, and installing and configuring an email client like `notmuch` or `mu4e` in Emacs. (Never could get OAUTH2 to work with `mbsync` so I had to settle for custom app passwords.)

My goal in setting Emacs as an email client is to have a long-term client-side solution for email, one that works the same way on MacOS, Linux, and Windows. Also, my hope was that it would integrate better with my workflow, which involves heavy use of Emacs `org-mode` and `org-roam`.

While I enjoy the simplicity of `mu4e`'s text interface, and search is way better than Thunderbird's search, rendering of html mails is suboptimal. There is probably a solution for this, it's just that I'm not willing to dive into another [time sink](https://code.zoia.org/posts/is-it-worth-the-time) for now. So I'm falling back to Thunderbird until I have time to fix it.
