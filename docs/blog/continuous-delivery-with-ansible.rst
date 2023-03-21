
Continuous Delivery and Rolling Upgrades with Ansible
#####################################################

While working on a application running on premises, I noticed that Ansible comes in handy to manage product upgrade
or automating the release pipeline. My starting point is Rest application implemented in JVM/Scala and running in 15 nodes
behind a HAProxy which provides high availability and load balancing. To be honest the deployment involves two data center
and a nginx proxy to balance the load between two data center, but it's not really relevant for the purpose of ansible use.


Background
************

The application is distributed as a binary zip tar ball, created by `Sbt native packager`_, and uploaded after every release
to an artifactory repository. The application package is a linux package binary application. Basically a zip with
all dependencies and an a runnable script. If one might question why not to use a fat jar instead you might want to read
`the-fault-in-our-jars-why-we-stopped-building-fat-jars`_. I had the same issue that in the post, my third parties dependencies overlap
META-INF/services and for me it's was a risk aggregating all dependencies jar in a fat jar.

The problem
************

Rolling up new software updates across 15 nodes in production with zero down time. My nodes are bare metal instances with static ips,
so for me ansible comes in handy to handle the deployment. In short we are going to use Ansible to automate follow steps:

1. Download binary application from artifactory.
2. Extract binary application to application home directory.
3. Update the soft link pointing to the new folder.
4. Restart systemd service.

We will create a ansible directory layout with role and tasks to manage new roll outs.

Let’s start by showcasing the folder structure that we should aim for.

.. literalinclude:: ./ansible/dir_tree.txt

In the folder structure above:

- ``production.yml`` ansible inventory for production nodes
- ``group_var/all.yml`` place holder file for common variables
- ``roles/rest-application`` ansible role which will handle the software upgrade
- ``rest-application.yml`` ansible playbook which binds them all.

Ansible inventory files
=======================

Ansible inventory represents a group of hosts that you want to automate tasks on. In my case a group of hosts tagged as "production environment"
where my application will run. Ansible supports inventory files in ini format or YAML format. I see more convenient and readable to use YML format.

The inventory production file looks like:

.. literalinclude:: ./ansible/production.yml
   :language: yaml

As one might notice the YML format allow to define and override ansible variables for all environment or per host.

At this point, if you have shared your ssh public key in target hosts, you could run a ping playbook ::

    $ ansible -i production.yml -m ping all

    node1.production.net | SUCCESS => {
      "changed": false,
      "ping": "pong"
    }



Ansible Roles
==============

Using ansible roles is kind of easy to automate the steps described above.

.. literalinclude:: ./ansible/roles/rest-application/tasks/main.yml
   :language: yaml


Ansible playbook
================

.. literalinclude:: ./ansible/rest-application.yml
   :language: yaml

Running the playbook
====================

When the ansible layout is ready you can run the playbook which just created ::

    $ ansible-playbook -i production.yml rest-application.yml


.. _Sbt native packager: https://www.scala-sbt.org/sbt-native-packager/formats/universal.html
.. _the-fault-in-our-jars-why-we-stopped-building-fat-jars: https://product.hubspot.com/blog/the-fault-in-our-jars-why-we-stopped-building-fat-jars