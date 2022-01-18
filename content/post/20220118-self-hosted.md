+++
title = "Self-hosted"
author = [ "Roberto Zoia"] 
date = 2022-01-18
draft = false
slug = "self-hosted"
tags = [ "self-hosted", "jamstack", "microservices" ]
+++

Some time ago I subscribed to `r/selfhosted`, a subreddit about "alternatives to popular online services that can be self-hosted without giving up privacy or locking you into a service you don't control."

It's difficult not to resonate with the ideals of the self-hosted movement: being in control of your data, retaining privacy, no vendor lock-in... As a [friend of mine](http://manoloalcazar.com) would say, _who can argue against freedom_? In practice, however, nowdays [people don't want to run their own servers](https://moxie.org/2022/01/07/web3-first-impressions.html), even if they know how to do it.

[^even-companies]: Companies also try not to run servers when possible, but hire services on the cloud instead.

For years I've hosted blogs on my own server. At different times I ran my own mail server. Not anymore. I don't want to run a server if there is an alternative. I'm migrating my sites to [Jamstack](https://jamstack.org/what-is-jamstack/) alternatives when possible.

For example, at the time of this writing this site is running on Netlify. Its content resides in a private Github repository, and Netlify automatically rebuilds the site using Hugo every time I publish a new article by pushing it to the repository. I don't need to manage nor do care which Linux distribution they are deploying. I don't need to apply the latest security patches to keep the OS up to date. I don't care if they are serving my content using Apache or other webserver. They provide the results I need.

For 2022, I'll migrate my [other other site](https://zoia.org) to Hugo, and publish it on Netlify or Vercel.

When possible, use a Jamstack or similar solution. Focus on delivering value, automate or delegate the rest.

