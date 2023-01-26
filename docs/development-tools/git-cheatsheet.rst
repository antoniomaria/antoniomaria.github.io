================
Git Cheat Sheet
================

This cheat sheet is not meant to be exhausted and only cover certain commands which are not
supported by any Git UI or integration is flaky and therefore you must use the git shell.

Git basis
***************

Define author name / email to be used for all commits in current repo or globally ::

    $ git config --global user.email "john.smith@qvantel.com"
    $ git config --global user.name "John Smith"

Git Reset
***************

Going back to the commit before HEAD. Won’t alter the working directory and the index ::

    git reset --soft HEAD^
    git reset --soft HEAD~1

Git submodules
***************

1. Clone a project witch has submodules

.. code-block:: bash

   $ git clone <repo> --recursive

2. Update and init submodules if you forget to do it when cloning

.. code-block:: bash

   $ git submodule update --init --recursive

3. Add a submodule to existing repository

.. code-block:: bash

   $ git submodule add -b <branch> <repo> my-submodule-name

4. Delete a submodule. Remove the submodule section from .gitmodules

.. code-block:: bash

   $ rm -rf .git/modules/submodule-name/
   $ git rm --cached submodule-name

5. Update submodule to latest commit. Assume that you have executed git init submodule before.

.. code-block:: bash

   $ cd submodule-name
   $ git checkout main
   $ git fetch
   $ git pull

   # Get back to project root
   cd ..
   git commit -am "Submodule updated to latest"