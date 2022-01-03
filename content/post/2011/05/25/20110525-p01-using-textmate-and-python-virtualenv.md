+++
title = "Using TextMate and Python's virtualenv"
date = "2011-05-25"
slug = "using-textmate-and-python-virtualenv"
tags = ["bundles", "python", "textmate", "TM_PYTHON", "virtualenv", "virtualenvwrapper"]
+++




[TextMate](http://macromates.com/) is a great text editor for MacOs.  But the default Python bundle does not recognize Python's virtual environments (`virtualenv`), which is rather annoying.

No need to modify your Textmate bundle.  This can be solved by declaring a project-specific shell variable named `TM_PYTHON` and assigning your virtualenv's custom python's path to it:

*   In TextMate, create a new project for your python program
*   Open the Project Drawer Window (View/Open Project Drawer)
*   Make sure no file is selected in the drawer. Click on the Get-Info icon to open the Project Information Dialog (see picture)
*   Add a variable named `TM_PYTHON` and assign it your virtualenv python path

(Your virtualenv python path can be obtained by typing `which python` in a Terminal window after activating your virtualenv environment with `workon`.)

![Creating the TM_PYTHON project-specific shell variable on TextMate](/media/2011/Screen-shot-2011-05-25-at-16.32.53.png)