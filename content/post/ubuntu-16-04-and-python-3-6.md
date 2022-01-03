+++
title = "Ubuntu 16.04 and Python 3.6+"
author = ["Roberto Zoia"]
date = 2021-11-09
draft = false
weight = 1001
+++

I was recently in the process of upgrading a system running Django 2.2 to 3.2. Django 3.2 requires Python 3.6+. This system is running on a cloud instance of Ubuntu 16.04, which only supports Python up to 3.5.

Upgrading the server to Ubuntu 18.04 or 20.04 is out of the question. (Just the thought of someone typing \`do-release-upgrade\` in a production server makes me shiver...) Also, the system is from a pre-docker era, so no luck there.

The cleanest way to run a more recent Python version is to install \`[pyenv\`](https://github.com/pyenv/pyenv). \`pyenv\` is a Python version management system which takes care of downloading, compiling, and installing the Python version you need without messing with the system configuration.

Python [now requires OpenSSL version 1.1.1+](https://docs.python.org/release/3.10.0/whatsnew/changelog.html#python-3-10-0-final), and Ubuntu 16.04 only provides OpenSSL up to version 1.0. So, if you try to install, for example, Python 3.10.0 using \`pyenv\`, you'll get an error complaining about OpenSSL. (The error is actually silent. You'll need to run \`pyenv\` with the verbose/-v in order to see the output.)

```nil
$ pyenv install -v 3.10.0


(Several lines and minutes later...)
ERROR: The Python ssl extension was not compiled. Missing the OpenSSL lib?

$
```

To fix this:

1.  Install OpenSSL 1.1.1 from [source](https://www.openssl.org/source/).
    -   Compile OpenSSL and install it.

<!--listend-->

```nil
$ wget https://www.openssl.org/source/openssl-1.1.1l.tar.gz
$ tar xvfz openssl-1.1.1l.tar.gz
$ cd openssl-1-1-1l
$ ./config
$ make
$ sudo make install
```

-   Add \`/usr/local/lib\` and \`/usr/local/local/lib64\` to your library path in \`.bashrc\` (or whatever your system uses) and reload your shell using \`$ exec $SHELL\`.

\#+begin-src
      export LD\_LIBRARY\_PATH=/usr/local/lib/:/usr/local/lib64:$LD\_LIBRARY\_PATH
\#+end\_src

-   Check that OpenSSL installed OK:

<!--listend-->

```nil
$ openssl version

OpenSSL 1.1.1l  24 Aug 2021
```

1.  Tell \`pyenv\` where are the OpenSSL files located so the compiler and liker can find them and then run \`pyenv\` to install the desired Python version.

<!--listend-->

```nil
$ export LDFLAGS="-L/usr/local/lib/ -L/usr/local/lib64/"
$ export CPPFLAGS="-I/usr/local/include -I/usr/local/include/openssl"
$ export PYTHON_CONFIGURE_OPTS="--enable-shared"
$ pyenv install -v 3.10.0
```

You should have now a working Python 3.10.0 that you can use with \`pyenv\`.
