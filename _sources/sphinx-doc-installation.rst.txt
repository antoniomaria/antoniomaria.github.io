How to create a static website with sphinx-docs
===============================================

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