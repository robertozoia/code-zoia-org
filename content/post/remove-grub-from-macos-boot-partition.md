+++
title = "Remove GRUB from MacOS boot partition"
author = ["Roberto Zoia"]
date = 2020-11-06
draft = false
+++

I've got Linux on an external SSD drive which I can boot from my Macbook Pro using `Command`-`D` while powering up to select Linux as the boot drive.

The only glitch is that when installing Linux, by mistake I installed GRUB (Linux boot loader) on my Mac root partition. The easiest way to fix this is to boot the machine into repair mode using `Command`-`R` and reinstall MacOS. This won't erase your data or applications, just reinstall the operating system and rewrite the boot partition. (The process takes about an hour, so plan ahead.)
