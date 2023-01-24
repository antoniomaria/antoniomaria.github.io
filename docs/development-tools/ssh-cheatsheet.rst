##################
SSH Cheat Sheet
##################

This cheat sheet is not meant to be exhausted and only include spells that a backend developer should
know on daily basis.

************************************************
Creating an SSH key pair for User Authentication
************************************************

Either if you need to commit to github, access to AWS EC2 instances, open a pull request to BitBucket
or where ever public key authentication is required you must create a key ssh key pair (public+private).
There are several algorithm type and key sizes supported for ssh-keygen which need to be selected depending
on the openssh version installed in the server you are trying to authenticate to.

According to `ssh-academy`_ ed25519 this is a new algorithm added in OpenSSH, and supported in github but in
legacy servers you might need to go for a legacy rsa algorithm.

Here it goes different keygen combinations depending on the algorithm selected::

    ssh-keygen -t ed25519 -C "your_email@example.com"
    ssh-keygen -t rsa -m PEM -C "your_email@example.com"
    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"


Your public/private pair will go to $HOME/.ssh directory. You will be prompt which file name to use
or id_ed25519, id_rsa depending on the algorithm selected.

Secure your private key
=======================

.. code-block:: bash

   $ .ssh $ chmod 600 id_rsa

Copying the Public Key to the Server
====================================

To use public key authentication, the public key must be copied to the server.::

    ssh-copy-id -i ~/.ssh/id_rsa user@host

Use by default your ssh key when accessing to any server
========================================================

In your .ssh/config ::

    Host *
      User ansanche
      IdentityFile ~/.ssh/id_rsa
      IdentitiesOnly yes
      PubkeyAcceptedAlgorithms +ssh-rsa
      HostkeyAlgorithms +ssh-rsa

or use specific key per server ::

    Host github.com
      Hostname github.com
      AddKeysToAgent yes
      IdentityFile ~/.ssh/id_ed25519

*********************
Creating SSH Tunnel
*********************

SSH tunnels come in handy when doing local development where you access to private resources. Typically you have databases
on cloud or private data centers with ip-filtering, or behind some firework which prevent using ordinary sql / nosql clients
from your laptop. The access to the private resources is allowed only to set of nodes which enough access right (for example
ec2 instances in the autoscaling group security group enabled to auroradb)

You can read more about the ssh tunnel motivation `ssh_tunnel`_:

Read from your consul instance, spring-boot configuration... which instance has access to database.

Verify that you have access to your ec2 instance which has access to DB ::

    ssh -i id_rsa ec2-user@EC2_IP_ADDRESS

Create ssh tunnel port forwarding ::

    ssh -i id_rsa -L 3306:RDS-HOST-NAME:3306 ec2-user@EC2_IP_ADDRESS

Once the tunnel is open you can access to private resource from localhost ::

    mysql -h 127.0.0.1 -P 3306 -u admin -p12345678

Ensure that you don't have a local mysql instance running in the same port ::

    lsof -i :3306

.. _ssh-academy: https://www.ssh.com/academy/ssh/keygen#creating-an-ssh-key-pair-for-user-authentication
.. _ssh_tunnel: https://aws.amazon.com/premiumsupport/knowledge-center/systems-manager-ssh-vpc-resources/