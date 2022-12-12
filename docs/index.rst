.. antonio coding notes documentation master file, created by
   sphinx-quickstart on Sun Dec 11 16:24:38 2022.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Bites of knowledge!
============================================

Hello there, my name is Antonio Sanchez and I am a software developer located in Finland. I do coding for a living, and learn
on the way. I am writing this for myself and for those who might find this site interesting.

To start with something, I would describe how I set up this site using sphinx and publish it to github pages. Enjoy

Create a site using sphinx-docs
============================================

Sphinx-docs is really popular in project documentation, I myself wanted to give a try also to write my own notes.
Because I would like to publish the site using github pages. I started checking out my own repository from git.
I assume you have installed python3 and pip.

1. Install sphinx

.. code-block:: bash

   $ pip install -U sphinx

2. Run sphinx-quickstart from the directory where pages will be generated.

.. code-block:: bash

    $ sphinx-quickstart
    > Separate source and build directories (y/n) [n]: y

3. Rename source directory to docs. Directory tree should look like:

.. code-block:: text

    |-- site
        |-- build
        |-- docs

4. Change source directory in Makefile

.. code-block:: text

    SPHINXOPTS    ?=
    SPHINXBUILD   ?= sphinx-build
    SOURCEDIR     = docs
    BUILDDIR      = build

5. You can already generate pages by running:

.. code-block:: bash

    $ make html
    Running Sphinx v5.3.0
    ...
    The HTML pages are in build/html.

6. If you like try to some of the sphinx themes

.. code-block:: bash

    pip install yummy-sphinx-theme

Edit the docs/conf.py as:

.. code-block:: text

    # -- Options for HTML output -------------------------------------------------
    html_theme = 'yummy_sphinx_theme'


Exploration
===========

.. toctree::
    :titlesonly:

    mac-os/index