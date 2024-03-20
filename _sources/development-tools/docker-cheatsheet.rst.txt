Docker Cheat Sheet
==================

This cheat sheet is not meant to be exhausted and only most frequently used command are included.

Docker install
---------------

Install Docker CLI ::

  brew install docker
  brew install docker-compose

Docker pull
------------

Pull default tag::

    $ docker pull alpine

    Using default tag: latest
    latest: Pulling from library/alpine
    a9eaa45ef418: Pull complete
    Digest: sha256:f271e74b17ced29b915d351685fd4644785c6d1559dd1f2d4189a5e851ef753a
    Status: Downloaded newer image for alpine:latest
    docker.io/library/alpine:latest

Docker run
-----------

Run container named test using the alpine:latest image. The -it instructs Docker to allocate a pseudo-TTY connected to
the container’s stdin; creating an interactive bash shell in the container. Container will be removed on exit

.. code-block:: bash

   $ docker run --rm --platform=linux/arm64 --name test -it alpine
   / # uname -a
   Linux 82b5a216c503 5.15.64-0-virt #1-Alpine SMP Mon, 05 Sep 2022 08:02:49 +0000 aarch64 Linux

Run a Docker container in the background, or detached mode.

.. code-block:: bash

   $ docker run -d --name my-apache-app -p 8080:80 httpd:2.4
   b914647c5233865c4f227a814a1d45978d95aea5d0bc50e6fce53d3c4b444a8b

Docker exec
------------

.. code-block:: bash

   docker exec -it my-apache-app bash

Docker rm
----------

Delete a container even running

.. code-block:: bash

   docker rm --force my-apache-app

Docker login
-------------
When using a private artifactory as a docker registry. First you need to login to avoid this error:

.. code-block:: bash

    Error response from daemon: Head "https://myartifactory/v2/kafka/manifests/latest": unknown: Props Authentication Token not found
    $ docker login artifactory.company.net -u user@domain.com -p base64passwd

Interesting links
*****************

* `<https://dzone.com/articles/docker-best-practices>`_
