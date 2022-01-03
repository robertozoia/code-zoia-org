---
title: "How to use Calibre with DeDRM tools on Linux to backup your Kindle library"
date: 2020-09-19T12:52:15-05:00
draft: false
toc: false
images:
tags:
  - drm
---

Amazon Kindle's ecosystem lets you buy an ebook and begin reading seconds after purchasing it. However, as most of Amazon's book are DRM-protected, you cannot make a backup of your library or convert your books´ format to read them on another platform. Companies come and go, and even if Amazon's is here for the long run, it's policies regarding how you can access the content your paid for may change in the future.

Using a Kindle app version prior to 1.26 On Windows or MacOs, you can use Calibre with Aprentice Alf's DeDRM plugin to convert the books from your Kindle app on your computer to a DRM-free format. The plugin automatically extracts the necessary key the Kindle app uses to encrypt your books and makes the process transparent.

On Linux, you can use Wine to install the Kindle app. However, the DeDRM plugin doesn't extract the decryption key automatically.  To extract the key, you need to install Python and PyCrypto in Wine and run `kindlekey.py` manually. Once you have the key, you can import it into Calibre using the DeDRM plugin.

I've tested the setup using Ubuntu 20.04.

1. Install [Calibre](https://calibre-ebook.com/) for Linux.

2. Download [Aprentice Alf's DeDRM tools](https://apprenticealf.wordpress.com/). Uncompress the file, open Calibre and install the DeDRM plugin.

3. Uncompress the DeDRM plugin file (`DeDRM_Plugin.zip`) and verify that there's a file named `kindlekey.py`.

4. Install `wine`:

```bash
$ sudo dpkg --add-architecture i386
$ sudo apt update
$ sudo apt install wine64 wine32
(...)
$ wine --version
wine-5.0 (Ubuntu 5.0-3ubuntu1)
```

5. Search on Google for the  Kindle app for Windows. You need version 1.26 or **earlier**. Install it using wine:

```bash
$ wine kindleforpc-installer-1.15.43061.exe
```

Run the Kindle app and register it with your Amazon account. You should be able to access your Kindle library without problems.

6. Download the most recent version of Python 2.7 **for Windows** from [Python.org](https://www.python.org/downloads/). Install it using wine:

```bash
$ wine msiexec /i python-2.7.18.msi
```

7. Download a [Windows installer for PyCrypto](http://www.voidspace.org.uk/python/modules.shtml#pycrypto) for Python 2.7. Install it using wine. (If you installed a 32-bit version of Python, use a 32-bit version of Pycrypto.)

```bash
$ wine pycrypto-2.6.win32-py2.7.exe
```

8. In the Linux terminal, naviagate to the folder where your `kindlekey.py` file resides. Then open a Windows shell using wine, and run kindlekey.py:

```bash
~/Downloads/DeDRM/original/DeDRM_tools_6.8.0/DeDRM_Plugin$ wine cmd.exe
Microsoft Windows 6.1.7601

D:(...) \DeDRM_Plugin>python kindlekey.py
Using Library AlfCrypto DLL/DYLIB/SO
searching for kinfoFiles in C:\users\(...)\Local Settings\Application Data
Found K4PC 1.9+ kinf2011 file: C:\users\(...)\Local Settings\Application Data\Amazon\Kindle\storage\.kinf2011
Decrypted key file using IDString '0' and UserName 'xxxxxxxxxx'

D:(...) \DeDRM_Plugin> exit
```

9. You should now have a file named `kindlekey1.k4i` in your directory. Open Calibre, click on the Preferences button. Navigate to Plugins/File Type. Locate the DeDRM plugin, and click the 'Customize Plugin' button and then click on `Kindle for Mac/PC ebooks`. Import the key into the DeDRM plugin and restart Calibre.

10. Locate your books inside the wine installation.  Wine stores the Windows installation under `~/.wine`. The Kindle books are usually located in `~/.wine/drive_c/users/[your username]/My Documents/My Kindle Content`.` I suggest you create a link to your Linux home directory.

You can now import books from your Kindle directory into Calibre, and make a DRM-free backup copy.


_Disclaimer_:  This instructions are intended for making a backup copy of your Kindle library, my intention is not to encourage piracy in any way.
