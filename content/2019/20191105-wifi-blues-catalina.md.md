+++
title = "Connecting to Public Wifi in MacOS Catalina"
date = "2019-11-05"
slug = "connecting-to-public-wifi-in-macos-catalina"
categories = ["macOS", ]
tags = ["catalina", "wifi"]
+++

After upgrading to MacOS Catalina, I could no longer connect to open WiFI networks, specifically hotel networks and coffee shops.  Previously, when connecting to one of these networks, a dialog would appear to ask for confirmation, a username/password combination, etc. No longer with Catalina.

After some extensive searching on the internet, the solution I found is launching the `Captive Network Assistant` manually. I wrote a small bash script to launch it from the command line on a terminal window:

```bash
#!/bin/bash

/System/Library/CoreServices/Captive\ Network\ Assistant.app/Contents/MacOs/Captive\ Network\ Assistant
```

(You should always use some kind of VPN when connecting to non-encrypted public networks.)