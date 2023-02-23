.. index:: Appendix
   :name: appendix

=========
Appendix
=========

The following sections will provide further details concerning the configuration and management of the IDPV eval environment.

.. toctree::
   :maxdepth: 1
   :hidden:
   :caption: Appendix



.. index:: Docker; Tips
   :name: appendix-docker

Docker
-------

.. highlight:: shell-session

**Docker Volumes**

Docker Containers are based on immutable **images** and different types of **volumes** where all variable data can be stored. For the eval scenario we use two types of such volumes:

* **Bind Mounts** - Used to map the ``config`` and ``hsm`` folders into the IDPV container
* **Volumes** - Used to store the MySQL DB in a volume called ``database`` that is fully managed by Docker itself

To **list the volumes** you can execute the following command::

   $ docker volume ls


**Docker Compose**

Docker Compose defines a set of services in a configuration file called ``compose.yaml``. This allows to pre-define all run parameters instead of adding them to a ``docker run`` command.

To **start all Docker services** in detached mode you simply run this command from the Docker Compose project folder::

   $ docker compose up -d

To **shut down and clean up all Containers** you run this command (Volumes have to be deleted separately)::

   $ docker compose down



.. index:: IDPV Server; Config
   :name: appendix-idpv-config

IDPV Server
------------

Some IDPV Server configuration parameters are not exposed to the external ``appsettings.yml`` file by default. However, the full list of attributes can be listed from the internal configuration file::

   $ more appsettings.json

So e.g. to **change the runtime value** of the API Key Expiry (default is 30 days) you could execute this command within the Container::

   $ sed -i 's|/"APIKeyExpiryInDays\": .*|/"APIKeyExpiryInDays/": 60,   //In Days |g' appsettings.json

As this change will only persist as long as the container exists you could also set the parameter in the ``appsettings.yml`` file by adding the following line::

   APIKeyExpiryInDays: 60            #In Days

This entry will overwrite the existing parameter with the same name in the ``appsetting.json``.



.. index:: MySQL; Useful Commands
   :name: appendix-mysql

MySQL
------

.. highlight:: MySQL

Useful Commands for MariaDB / MySQL


List Databases::

   > SHOW DATABASES;

List Database Users::

   > SELECT user,host FROM mysql.user;

List User Rights::

   > SHOW GRANTS FOR idpvuser;

Create IDPV User::

   > CREATE USER idpvuser IDENTIFIED BY 'mysqluser4idpv';

Assign IDPV User Rights::

   > GRANT SELECT, INSERT, UPDATE, DELETE, CREATE, REFERENCES, INDEX, ALTER ON IDPrimeVirtualServer.* TO idpvuser;

Change Password::

   > ALTER USER idpvuser IDENTIFIED BY 'mysqluser4idpv';

Delete User::

   > DROP USER idpvuser;

Delete Data Base ::

   > DROP DATABASE IDPrimeVirtualServer;

Select data base for further usage::

   > USE IDPrimeVirtualServer;

List tables of selected data base::

   > SHOW TABLES;

List column names of a table::

   > DESCRIBE <table_name>;
    
List table entries::

   > SELECT * from <table_name>;

List the existing tenant name and IDs::
    
   > select TenantName,TenantID from Tenant; 

