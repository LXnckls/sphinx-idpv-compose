.. index:: Docker; Compose
   :name: docker-compose

=============================
Setup Docker Compose
=============================

For the eval scenario you need to install a **Docker Compose** environment.

The easiest way to get a current Docker system is to install `Docker Desktop <https://www.docker.com/get-started/>`_.

.. note:: **Docker Desktop** is free of charge for personal use only!


Docker on Ubuntu
-----------------

On Ubuntu you have to execute the steps outlined in the `Docker documentation <https://docs.docker.com/engine/install/ubuntu/>`_ to add the Docker repository. Here is a short summary.

First you have to make sure that any **older version of Docker is fully removed** which sometimes is pre-installed on Ubuntu::

   $ sudo apt-get remove docker docker-engine docker.io containerd runc

Then you **add the Docker repository**::

   $ sudo apt-get update

::

   $ sudo apt-get install ca-certificates curl gnupg lsb-release

::

   $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker.gpg

::

   $ echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

::

   $ sudo apt-get update

In the last step you have to **install the latest version of Docker** from the new repository::

   $ sudo apt-get install docker-ce docker-ce-cli containerd.io docker-compose-plugin

The following command will **run your first container** to verify that Docker is fully up and running::

   $ sudo docker run hello-world



Prepare Compose Environment
----------------------------

For the IDPV eval you should **create a project folder** with the following folder structure:

* ``idpv-eval`` - Root of your Docker Compose folder and therefore the default project name

  * ``idpv`` - Config folder for IDPrime Virtual Server

    * ``config`` - IDPV Server configuration files
    * ``hsm`` - HSM configuration files for IDPV Server

To prepare the Docker Compose settings you have to download the :download:`compose.yaml </_static/compose.yaml>` and store it in the root of your project directory.

