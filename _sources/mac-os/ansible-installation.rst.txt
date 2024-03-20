==================================
Ansible installation on ARM macOS
==================================

Ansible I think, no needs any formal presentation, is a automation tool that automates infrastructure tasks.
Restart services, install software, create directories, delete temporary files ... everything you can do on
ssh shell on a single host, can be automated to ansible plays and performed to many hosts, in a composable
and OS agnostic fashion.

Installation using pip
************************

Before hitting the spell ``pip install ansible`` which will install the latest ansible version using the default
python / pipe installation. I will suggest to install ``pyenv`` and create virtual environments, so you don't mess
with OS python installation. See :ref:`pyenv-installation`

.. code-block:: bash

    pip install ansible