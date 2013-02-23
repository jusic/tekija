.. you can compile a version of this text using rst2html.py, see docutils.sf.net


Järkeä tekijänoikeuslakiin
==========================

This is the public source code for the Finnish copyright law 
citizen initiative campaign "Järkeä tekijänoikeuslakiin" ("Common sense into
copyright law").

http://www.jarkeatekijanoikeuslakiin.fi / http://www.jarkea.fi / `http://www.järkeä.fi`_

.. _`http://www.järkeä.fi` : http://www.järkeä.fi


Installation
------------

In order to compile the static pages, you need to install staticjinja.
The recommended approach is to use Python virtualenv, so that you can 
leave your system Python installation intact. We use Python 2.7 currently.

#. Install Python 2.7 and virtualenv.
#. Clone the repository by running ``git clone git@github.com:jusic/tekija.git``
#. Under the cloned repository directory, run ``virtualenv venv``. (On Windows, if you don't have virtualenv in your PATH, run e.g. ``C:\Python27\Scripts\virtualenv.exe venv``)
#. Activate the new virtualenv by running ``venv/bin/activate``. (On Windows, run ``venv\Scripts\activate``.
#. Install staticjinja and other required packages to the virtualenv by running ``pip install -r requirements.txt``.


Usage
-----

To compile the static html versions of the web page, run ``python build.py``. 
This will create ``en/``, ``fi/`` and ``sv/`` directories to the main root.

The main root ``index.html`` redirects to ``fi/index.html``.


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


Development
-----------

Contributions are warmly welcome, send pull requests on GitHub. 

To hack the site further, edit the page templates under ``templates/`` 
directory. 


Few guidelines for development:

- Please try to keep the translations in sync, whatever you do. 
  If you can't translate your changes properly, please mark respective 
  passages untranslated in your edited text.

- Please respect copyright and other laws. 

- Please attribute all quotations properly. 

- If you add pictures, please make sure that they are properly downsized.
  (I will not allow big pictures (>100-200kB) to the repository.)
