+++
title = "Python Whatsapp Client Blues"
date = "2017-09-19"
slug = "python-whatsapp-blues"
+++



I had the idea to code a simple script in Python that would notify of the day's birthdays to a Whatsapp number or a Whatsapp group.

WhatsApp has no public API (that I'm aware of...)  I spent some time with [YowSup](https://github.com/tgalal/yowsup), which didn't work with the examples of their own page.  After applying some changes suggested in the YowSup forums, I was able to register my cel number and obtain a password for the account.

However, I'm dropping the script for now. Using YowSup would imply that every time WhatsApp changes their MD5 hashes and signatures (probably every time they update their client), my script would stop working.