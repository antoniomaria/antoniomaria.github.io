==============================================
How to install Java SDK on macOS
==============================================

How to install Java SDK on macOS using homebrew
***********************************************

1. Prerequisite install home brew if you haven't yet installed it

.. code-block:: bash

   $ xcode-select --install
   $ $ curl -fsSL -o install.sh https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh

Add later on to your .bash_profile

.. code-block:: bash

   eval "$(/opt/homebrew/bin/brew shellenv)"

See more `install-homebrew-on-mac`_.

2. Add the casks tap

.. code-block:: bash

   $ brew tap homebrew/cask-versions
   $ brew tap homebrew/cask

3. Look for installable versions

.. code-block:: bash

   $ brew search java
   $ brew search temurin

4. Install a specific version of the JDK such as java11, temurin8, temurin11, temurin17,
   or just java or temurin for the most current of that distribution. For example:

.. code-block:: bash

    $ brew install java
    $ brew install --cask temurin

    $ brew install --cask temurin17
    ==> Downloading https://github.com/adoptium/temurin17-binaries/releases/download/jdk-17.0.6%2B10/OpenJDK17U-jdk_aarch64_mac_hotspot_17.0.6_10.pk
    ######################################################################## 100.0%
    ==> Installing Cask temurin17
    ==> Running installer for temurin17; your password may be necessary.
    Package installers may write to any location; options such as `--appdir` are ignored.
    Password:
    installer: Package name is Eclipse Temurin
    installer: Installing at base path /
    installer: The install was successful.
    🍺  temurin17 was successfully installed!

And these will be installed into /Library/Java/JavaVirtualMachines/

.. code-block:: bash

   /usr/libexec/java_home -V
   /usr/libexec/java_home -v 8

You should have something like:

*  /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home
*  /Library/Java/JavaVirtualMachines/openjdk-11.jdk/Contents/Home
*  /Library/Java/JavaVirtualMachines/temurin-17.jdk/Contents/Home
*  /opt/homebrew/Cellar/openjdk@11/11.0.16.1_1/libexec/openjdk.jdk/Contents/Home

Switch Java versions with Jenv
*********************************************

1. Install Jenv

.. code-block:: bash

   $ brew install jenv
   To activate jenv, add the following to your /Users/jhon.smith/.bash_profile:
   export PATH="$HOME/.jenv/bin:$PATH"
   eval "$(jenv init -)"

1. Add java versions to Jenv

.. code-block:: bash

   $ jenv add /Library/Java/JavaVirtualMachines/zulu-8.jdk/Contents/Home
   $ jenv add /Library/Java/JavaVirtualMachines/openjdk-11.jdk/Contents/Home
   $ $ jenv versions
    * system (set by /Users/jhon.smith/.jenv/version)
    1.8
    1.8.0.312
    11.0
    11.0.16.1
    17.0
    17.0.6
    openjdk64-11.0.16.1
    zulu64-1.8.0.312

You can set the default jvm with the command:

.. code-block:: bash

    $ jenv global 1.8

To make sure JAVA_HOME is set, make sure to enable the export plugin:

.. code-block:: bash

    $ jenv enable-plugin export

References
*********************************************

.. _install-homebrew-on-mac: https://iboysoft.com/howto/install-homebrew-on-mac.html

.. target-notes::