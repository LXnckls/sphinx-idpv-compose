.. index:: Data Base, MySQL
   :name: db

==========================
Prepare Data Base
==========================

.. highlight:: shell-session

IDPV supports several data bases products. This eval setup uses a **Docker version of MySQL**.

To setup and **configure the MySQL Container** you can start it with the following Docker Compose command (make sure you have your project setup as described in :ref:`docker-compose`)::

   $ docker compose up -d db

Now you can start a ``bash`` **shell** in the new Container::

   $ docker exec -it mysql bash

.. highlight:: mysql

**Login to MySQL** using the password specified in :download:`compose.yaml <_static/compose.yaml>`::

   $ mysql --password=mysqlroot4idpv

**Create** a new data base::

   mysql> CREATE DATABASE IDPrimeVirtualServer;

Then **create a db user** with the necessary rights and confirm the changes::

   mysql> CREATE USER 'idpvuser' IDENTIFIED BY 'mysqluser4idpv';

::

   mysql> GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, REFERENCES, INDEX, ALTER ON IDPrimeVirtualServer.* TO 'idpvuser';

::

   mysql> FLUSH PRIVILEGES;

