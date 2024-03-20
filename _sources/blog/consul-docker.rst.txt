
Consul on Docker
#####################################################

If you are working on a distributed application where every service has many instances, or more likely you have many
services, you might be using Consul as a service discovery (DNS lookup) or Consul Key-Value store so the configuration
and secrets are not part of the service.

This post will explain you how to get started with consul, and key value store with Docker compose.

Start consul using docker
-------------------------

There are number of ways to get consul container running locally, one of the easies is using docker-compose like described
in `learn-consul-docker`_ .

.. _learn-consul-docker: https://github.com/hashicorp/learn-consul-docker

.. code-block:: yaml

    version: '3.7'

    services:

      consul-server:
        image: hashicorp/consul:1.15.1
        container_name: consul-server
        restart: always
        volumes:
         - ./server.json:/consul/config/server.json:ro
        networks:
          - consul
        ports:
          - "8500:8500"
          - "8600:8600/tcp"
          - "8600:8600/udp"
        command: "agent"

    networks:
      consul:
        driver: bridge

Remember to create a file server.json at the same level that your docker-compose.yml with default configuration

.. code-block:: json

    {
        "node_name": "consul-server",
        "server": true,
        "bootstrap" : true,
        "ui_config": {
            "enabled" : true
        },
        "data_dir": "/consul/data",
        "addresses": {
            "http" : "0.0.0.0"
        }
    }

Start the consul by running docker-compose:

.. code-block:: bash

    $ docker-compose up

    Container consul-server             Created                                                                                                                                                                                     0.0s
    ..
    consul-server  | ==> Starting Consul agent...
    consul-server  |               Version: '1.15.1'
    consul-server  |            Build Date: '2023-03-07 20:35:33 +0000 UTC'
    consul-server  |               Node ID: 'c581f5bd-d05f-17c3-4e3e-daf3af8d1401'
    consul-server  |             Node name: 'consul-server'
    consul-server  |            Datacenter: 'dc1' (Segment: '<all>')
    consul-server  |                Server: true (Bootstrap: true)

See more references
~~~~~~~~~~~~~~~~~~~

* `<https://alesnosek.com/blog/2017/07/15/first-look-at-the-key-value-store-in-consul/>`_



