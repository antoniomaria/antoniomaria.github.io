==============================================
How to install MySQL on macOS
==============================================

**********************************************
How to install MySQL on macOS using homebrew
*********************************************

1. Install mysql from a terminal shell

.. code-block:: bash

   $ brew install mysql
   ==> mysql
   We\'ve installed your MySQL database without a root password. To secure it run:
   mysql_secure_installation
§
2. Starts a mysql instance

.. code-block:: bash

   $ mysql.server start
   Starting MySQL
   . SUCCESS!

3. Set root MySQL password
   The mysql_secure_installation utility validates how strong is the password, disable/enable root access from remote etc. For development purposes this is enough:
   mysql_secure_installation

.. code-block:: bash

   $ mysqladmin -u root password 'topsecret'

4. Access MySQL on mac

.. code-block:: bash

   $ mysql -u root -p


*********************************************
Operation commands
*********************************************

Stop MySql instance
---------------------

.. code-block:: bash

   $ mysql.server stop

Run MySql as service
---------------------

.. code-block:: bash

    $ brew services start mysql

Stop MySql on Mac start
------------------------

If you don't want MySQL service to start every time you start your mac then run the below command

.. code-block:: bash

    $ brew services start mysql