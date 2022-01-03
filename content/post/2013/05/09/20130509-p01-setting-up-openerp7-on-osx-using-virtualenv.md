+++
title = "Setting up an OpenERP v7 development environment on OSX using virtualenv"
date = "2013-05-09"
slug = "setting-up-openerp7-on-osx-using-virtualenv"
tags = ["openerp", "virtualenv", "python"]
+++






Nowdays I develop mostly on OSX using Python.  I am particularly fond of using virtualenv and virtualenvwrapper for keeping separate environments for each project, so that the system's Python distribution does not get contaminated with the project dependencies.  (This also helps in having a clear set of library dependencies when deploying the project to a production server.)

Some days ago, while trying to set up a development environment[^3] for OpenERP v.7, I found that most of the OpenERP tutorials and manuals are centered on Linux, and only consider system-wide installation of the required libraries.

Here are the steps I followed to get OpenERP running on OSX 10.8.3.

### 1. Setup a virtualenv for your project

```bash
$ mkvirtualenv openerp-dev
```

### 2. Tell your environment which architecture you are compiling your modules for

(Without this line some modules with throw errors while installing.)

```bash
$ export ARCHFLAGS='-arch i386 -arch x86_64'
```
### 3. Install OpenERP dependencies

Most of the dependencies can be installed on your virtualenv using pip[^1]:

```bash
$ pip install python-dateutil feedparser gdata \
python-ldap lxml mako python-openid \
psycopg2 Babel reportlab simplejson \
pytz vatnumber vobject python_webdav \
Werkzeug pyparsing==1.5.7 pydot \
PyYAML xlwt ZSI PIL
```


Other dependencies must be installed by hand.

<b>pychart</b>

Download PyChart from <http://download.gna.org/pychart/PyChart-1.39.tar.gz> and install it into your virtual environment:

```bash
$ wget http://download.gna.org/pychart/PyChart-1.39.tar.gz
$ tar xvfz PyChart-1.39.tar.gz
$ python setup.py build
$ python setup.py install
```

<strong>libxslt1</strong>

libxslt1 is included in the libxml2 library bindings for python.  Download libxml2 from xmlsoft.org:

```bash
$ wget ftp://xmlsoft.org/libxml2/python/libxml2-python-2.6.11.tar.gz
$ tar xvfz libxml2-python-2.6.11.tar.gz
$ cd libxml2-python-2.6.11
$ python setup.py build
$ python setup.py install
```

### 4. Install OpenERP from launchpad

If you don't have <b>bazar</b> installed in your Mac, you can do it easily using [brew](http://mxcl.github.io/homebrew/):

```bash
$ brew install bzr
```
Download OpenERP v7 server, addons and web addons from the development trunk of the [OpenERP Project Group on launchpad](https://launchpad.net/openobject) using bazar (this can take some time):

```bash
$ bzr lp:openobject-server/7.0          #  Server
$ bzr branch lp:openobject-addons/7.0   #  Server addons
$ bzr branch lp:openerp-web/7.0         #  Web interface and addons
```

Change into the `openerp-tools` directory and use `make` to download OpenERP v7:

```bash
$ make init-v70
$ cd server
```

Install OpenERP into your Python environment.  The setup script will pull automatically any missing dependencies.

```bash
$ python setup.py install
```

Start OpenERP server and instruct the server to create a sample configuration file for us. (The file will be named `.openerp_serverrc` and will be created in your user's home directory.)

```bash
$ ./openerp-server -s
```

### 5. Change OpenERP's configuration file to reflect you development setup

Using your favorite editor, open `~/.openerp_serverrc`. The minimum changes required for OpenERP to start are:

<b>PostgreSQL connection parameters</b>

```bash
db_host = localhost    # (or an IP)
db_maxconn  = 64
db_name     = False     # don't need to specify a database name
db_password = your_db_user_password
db_port     = 5432
db_template = template1
db_user     = your_db_user
```
<b>Server addons and web addons location</b>

```bash
addons_path = /Users/(...)/openerp-tools/addons/,/Users/(...)/openerp-tools/web/addons/
```

Note that there are no spaces between paths, just a comma. (It took me some time to figure out why my paths were not being recognized by OpenERP.)

### 6. Start your OpenERP server using your configuration file

```bash
$ ./openerp-server -c /path/to/.openerp_serverrc
```
Launch your favorite browser and point to localhost:8069, and you should see the OpenERP login screen.



[^1]:  This list was extracted from [OpenERP dependencies for Linux](http://doc.openerp.com/v6.1/install/linux/server/index.html#installing-the-required-packages). PyParsing version is important because versions higher than 1.5.7 are for Python 3.

[^3]: OpenERP in this development environment runs in a terminal shell, as opposed to a production webserver like Apache.
