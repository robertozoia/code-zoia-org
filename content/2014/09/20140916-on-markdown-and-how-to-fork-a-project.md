+++
title = "On Markdown and how to fork a project"
date = "2014-09-15"
tags = ["markdown"]
slug = "on-markdown-and-how-to-fork-a-project"
+++



[Markdown](http://daringfireball.net/projects/markdown/) and its [syntax specification](http://daringfireball.net/projects/markdown/syntax) were developed by John Gruber as a text-to-HTML conversion tool for webwriters.  Over the years, it has been widely adopted by sites likes GitHub and StackExchange. Most programming languages have some kind of Markdown library available, always developed not by Gruber but by some third party.

The syntax for Markdown hasn't been updated in years.  Different implementations implement Markdown different... and output different HTML code for the same markdown.  Jeff Atwood (Coding Horror), John MacFarlane and others have launched an initiative to work around the limits of the current Markdown specification.  Jeff Atwood explains their motivations in his [post standard flavored markdown](http://blog.codinghorror.com/standard-flavored-markdown/).

The 'problem' is they chose to name their project _Standard Markdown_.  After a mail from John Gruber stating that he found the name inappropiate, they renamed it to [_Common Markdown_](http://blog.codinghorror.com/standard-markdown-is-now-common-markdown/), which doesn't seem adequate either.

I think standarizing Markdown is the correct thing to do.   But if the initiative does not come from the project owner, the way to _standarize_ an open source project is to fork it and change its name to whatever you want.


