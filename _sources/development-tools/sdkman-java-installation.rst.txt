==================================
How to install SDKMan on macOS
==================================

SDK man installation is OS agnostic and it has support for Unix based distribution like described in:
https://sdkman.io/install

How to install Java with SDKMan
***********************************************

1. Show posible java candidates

.. code-block:: bash

   $ sdk list java
   $ ================================================================================
    Available Java Versions for macOS ARM 64bit
    ================================================================================
     Vendor        | Use | Version      | Dist    | Status     | Identifier
    --------------------------------------------------------------------------------
     Corretto      |     | 20           | amzn    |            | 20-amzn
                   |     | 20.0.1       | amzn    |            | 20.0.1-amzn
                   |     | 19.0.2       | amzn    |            | 19.0.2-amzn
                   |     | 19.0.1       | amzn    |            | 19.0.1-amzn

2. Install the latest

.. code-block:: bash

   $ sdk install java

3. Optinally install java 8

.. code-block:: bash

   $ sdk install java 8.0.362-zulu



Switch Java versions with SDK environments
*********************************************

1. Set a sdk environment to your folder

.. code-block:: bash

   $ sdk env init
   .sdkmanrc created.

2. Modify the sdkmanrc file according to the java version you want to specify

.. code-block:: bash

   $ cat .sdkmanrc
    # Enable auto-env through the sdkman_auto_env config
    # Add key=value pairs of SDKs to use below
    java=8.0.362-zulu

3. Active the sdk environment whenever you need to change java version for the current shell session

.. code-block:: bash
    $ % sdk env

    Using java version 8.0.362-zulu in this shell.


References
*********************************************

.. _install-homebrew-on-mac: https://iboysoft.com/howto/install-homebrew-on-mac.html

.. target-notes::