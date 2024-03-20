==============================================
How to install MySQL on macOS
==============================================

How to install MySQL on macOS using homebrew
*********************************************

1. Install mysql from a terminal shell

.. code-block:: bash

   $ brew install mysql
   ==> mysql
   We\'ve installed your MySQL database without a root password. To secure it run:
   mysql_secure_installation

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


Installation details
*********************************************

.. code-block:: bash

    $ brew list mysql
    /opt/homebrew/Cellar/mysql/8.0.31/.bottle/etc/my.cnf
    /opt/homebrew/Cellar/mysql/8.0.31/bin/
    /opt/homebrew/Cellar/mysql/8.0.31/bin/mysql
    /opt/homebrew/Cellar/mysql/8.0.31/bin/mysql.server
    /opt/homebrew/Cellar/mysql/8.0.31/bin/mysql_client_test
    /opt/homebrew/Cellar/mysql/8.0.31/bin/mysql_config
    /opt/homebrew/Cellar/mysql/8.0.31/bin/
    /opt/homebrew/Cellar/mysql/8.0.31/homebrew.mysql.service
    /opt/homebrew/Cellar/mysql/8.0.31/lib/ (3 other files)
    /opt/homebrew/Cellar/mysql/8.0.31/share/
    /opt/homebrew/Cellar/mysql/8.0.31/support-files/ (3 files)
    /opt/homebrew/etc/my.cnf

.. code-block:: bash

    $ cat /opt/homebrew/etc/my.cnf
    # Default Homebrew MySQL server config
    [mysqld]
    # Only allow connections from localhost
    bind-address = 127.0.0.1
    mysqlx-bind-address = 127.0.0.1
    secure-file-priv=


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

Import CSV or restoring a backup up
-----------------------------------
While trying to import a CSV on a mysql instance, noticed that mysql check if folder where backup is located is secure. This property is determine by
`secure-file-priv`_. Set to empty to disable the validation on my.conf, or copy your files to default folder. In DEB, RPM, SLES, SVR4 based distro default is /var/lib/mysql-files.
In macOS default is NULL, which means import and exports operation are disabled.

.. code-block:: bash

    $ cat mydump.txt
    LOAD DATA INFILE 'output-00001.csv' INTO TABLE employee FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n' IGNORE 1 ROWS (id,name, age);
    $ mysql -u root -p hpd < mydump.sql


References
*********************************************

* See more `how-install-mysql-macos-homebrew`_.

.. _how-install-mysql-macos-homebrew: https://www.novicedev.com/blog/how-install-mysql-macos-homebrew
.. _secure-file-priv: https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html#sysvar_secure_file_priv

.. target-notes::