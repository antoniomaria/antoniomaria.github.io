==================
Python on M1 macOS
==================

Sooner than later as a mac user will end up using python, and you ask your self this question

Which Python am I using?
************************

Or most specifically which python interpreter is used when a run a Python based program (like ansible). You will likely have
available ``python3`` in a M1 based macOs. But python2 is not available any more

.. code-block:: shell
    :linenos:

    QFINM377:~ antonio.sanchez$ type python3
    python3 is /usr/bin/python3

Installing and switching different Python versions
*****************************************************

Python is an interpreted language an opposite to GoLang, or Java, so in case that your python application needs some
dependencies (requirements.txt) is advisable to not to mess with built-in python interpreter when you use pip install.
https://github.com/pyenv/pyenv does a incredible job installing and switching python versions without a pain.

Install pyenv like described ::

    brew update
    brew install pyenv

Double check that pyenv is installed in ``$HOME/.pyenv``

Add in your ``.bash_profile`` and reload with ``source .bash_profile``.

.. code-block:: shell
    :linenos:

    export PYENV_ROOT="$HOME/.pyenv"
    command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
    eval "$(pyenv init -)"


Now you can install phyton2 and python3 and switch between them


.. code-block:: shell
    :linenos:

    pyenv install --list
    pyenv install 3.10.6
    pyenv install 2.7.18
    pyenv global 3.10.6

Virtual environments using pyenv
*********************************

Create and use virtual environment.

.. code-block:: shell
    :linenos:

    pyenv virtualenv my-python-app-env

    pyenv activate my-python-app-env

    # installed requirements
    pip install -r my-python-app-dependencies.pip