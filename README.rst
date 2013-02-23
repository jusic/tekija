.. you can compile a version of this text using rst2html.py, see docutils.sf.net
.. $ rst2html.py README.rst > README.html

Järkeä tekijänoikeuslakiin
==========================

This is the public source code for the Finnish copyright law 
citizen initiative campaign "Järkeä tekijänoikeuslakiin" ("Common sense into
copyright law").

The campaign web site can be found at:

http://www.jarkeatekijanoikeuslakiin.fi / http://www.jarkea.fi / `http://www.järkeä.fi`_

.. _`http://www.järkeä.fi` : http://www.järkeä.fi

The webserver on that address runs ``nginx``, which serves purely static 
web pages.


Installation
------------

In order to compile the static pages, you need to install staticjinja.
The recommended approach is to use Python virtualenv, so that you can 
leave your system Python installation intact. We use Python 2.7 currently.

#. Install Python 2.7 and virtualenv.
#. Clone the repository by running ``git clone git@github.com:jusic/tekija.git``
#. Under the cloned repository directory, run ``virtualenv venv``. (On Windows, if you don't have virtualenv in your PATH, run e.g. ``C:\Python27\Scripts\virtualenv.exe venv``.)
#. Activate the new virtualenv by running ``venv/bin/activate``. (On Windows, run ``venv\Scripts\activate``.)
#. Install staticjinja and other required packages to the virtualenv by running ``pip install -r requirements.txt``.


Usage
-----

To compile the static html versions of the web page, activate the 
virtualenv environment (see 4. above) and run ``python build.py``. 
This will create ``en/``, ``fi/`` and ``sv/`` directories to the 
``static-output`` directory.

The root ``index.html`` inside ``static-output`` redirects to ``fi/index.html``.


Contributing
------------

Contributions are warmly welcome. Fork this repository on GitHub and send pull 
requests. Alternatively, you can add your contributions and requests to the 
project `issue tracker`_ on GitHub.

See `TODO.rst`_ and `issue tracker`_ for open tasks.

.. _`TODO.rst`: https://github.com/jusic/tekija/blob/master/TODO.rst
.. _`issue tracker`: https://github.com/jusic/tekija/issues

To hack the site further, edit the page templates under ``templates/`` 
directory. The base template is found under ``template/_base.html``. All
files prefixed with underscore are not compiled directly, but instead used
by other pages.

All CSS, JavaScript and possible image files are meant to be put under 
``static-output/`` directory.


Few guidelines for development:

- **Be concise.** Keep in mind, that this is the campaign entry page 
  for everybody, including the uninitiated. 

- **Be civil and nice.** Please respect copyright and other laws, 
  set a good example.

- Please try to **keep the translations in sync**, whatever you do. 
  If you can't translate your changes properly, please mark respective 
  passages untranslated in your edited text.

- Please **attribute all quotations properly**. If you translate quotations,
  mark it as well clearly.

- If you add pictures, please make sure that they are properly downsized.
  (I will not allow big pictures (>100-200kB) to the repository.)


Troubleshooting
---------------

**Running build.py gives** 
``TypeError: writelines() argument must be a sequence of strings``.

This is probably a bug in staticjinja 0.0.8 or jinja2 2.6, which prevents 
writing unicode characters (i.e. scandinavian alphabet) in the templates. 
For a quick-and-dirty fix for this, manually patch the file
``venv/lib/python2.7/site-packages/jinja2/environment.py`` around line 1053
from:

 :: 
  
  def dump(self, fp, encoding=None, errors='strict'):

to:

 ::

  def dump(self, fp, encoding="utf-8", errors='strict'):

A better fix for this is welcome, and please send it to upstream as well. 
One possibility is to patch the staticjinja code which calls this function.


